---
title: \[Android] Parcelable 간단 예제
classes : wide
date: '2021-04-13T02:05:00.004-07:00'
categories : 
- android
tags:
- android
modified_time: '2021-04-16T18:03:35.260-07:00'
blogger_id: tag:blogger.com,1999:blog-3133736334944064054.post-5786560968529469240
blogger_orig_url: https://lugan-study-it.blogspot.com/2021/04/parcelable.html
---
Parcelable 간단 예제
-----
```java
 public class SimpleData implements Parcelable {
 
    String name;
 
    int number;
 
    TestData testdata;
 
 
 
    public SimpleData(String name, int number) {
 
        Log.d("테스트","public SimpleData(String name, int number){\nthis.name = name;\nthis.number = number;}");
 
        this.name = name;
 
        this.number = number;
 
    }
```

<br>

```java
    //parcel 에다가 데이터 저장함. 굳이 name number 아니여도 아무거나 다됨. 예를들어 bluteGatt 객체면 Gatt.uuid, Gatt.bluetooth 모듈 등등
 
    //bluetooth gatt 객체는 pacelable 을 지원하며, parcel 안쓰는게 좋다고함. 싱글톤으로 접근하는게 좋다고함.
 
    @Override
 
    public void writeToParcel(Parcel parcel, int flags) {
 
        Log.d("테스트","\nwriteToParcel(Parcel parcel, int flags){\nparcel.writeString(name);\nparcel.writeInt(number);}");
 
        parcel.writeString(name);
 
        parcel.writeInt(number);
 
    }
 
 
 
    //createFromParcel 에서 실행, parcel에서 String, read 읽고 SimpleData 그자체를 리턴함
 
    protected SimpleData(Parcel parcel) {
 
        Log.d("테스트","\nSimpleData(Pacel parcel){\nname = pacel.readString();\nnumber = parcel.readInt();}");
 
        name = parcel.readString();
 
        number = parcel.readInt();
 
    }
 
    @Override
 
    public int describeContents() {
 
        Log.d("test","describeContents() -> return 0;");
 
        return 0;
 
    }
 
    /*
    parcel.readvalue(Classloader loader);
    구획에서 입력된 객체를 읽습니다. 지정된 클래스 로더는 동봉된 'Parcelables'를 로드하는 데 사용됩니다. Null이면 기본 클래스 로더가 사용됩니다.
    parcel.dataCapacity();
    구획의 총 공간을 반환합니다. 항상 >= dataSize입니다. 데이터 크기와 데이터 크기()의 차이는 구획이 데이터 버퍼를 재할당해야 할 때까지 남은 공간의 양입니다.
    parcel.dataAvail();
    구획에서 읽을 남은 데이터 양을 반환합니다. 즉, dataSize-dataPosition입니다.
    parcel.setDataCapacity(int size);
    구획의 용량(현재 사용 가능한 공간)을 변경합니다.
    parcel.recycle();
    'Parcel 객체'를 다시 '풀'에 넣습니다. 이 호출 후에는 개체를 만지면 안 됩니다. (메모리 해제인듯?)
    parcel.marshall();
    'parcel'의 원시 바이트를 반환합니다.
    여기서 검색하는 데이터는 로컬 디스크, 네트워크를 통해 어떤 종류의 영구 저장소에도 저장해서는 안 됩니다.
    그러려면 표준 직렬화 또는 다른 종류의 일반 직렬화 메커니즘을 사용해야 합니다.
    'Parcel marshalled representation'은 로컬 IPC에 매우 최적화되어 있으므로 플랫폼의 다른 버전에서 생성된 데이터와의 호환성을 유지하려고 하지 않는다.
    */
 ```

<br>
<br>

 ```java
     public static byte[] Serialiazing_TestData(String name, int age, String text){
 
        byte[] SreializedTestData = null;
 
        try {
 
            ByteArrayOutputStream byteArrayOutputStream = new ByteArrayOutputStream();
 
            ObjectOutputStream objectOutputStream = new ObjectOutputStream(byteArrayOutputStream);
 
 
 
            TestData testData = new TestData(name, age, text);
 
            objectOutputStream.writeObject(testData);
 
            SreializedTestData = byteArrayOutputStream.toByteArray();
 
            return SreializedTestData;
 
        } catch (Exception e) {
 
            e.printStackTrace();
 
        }
 
        return SreializedTestData;
    }
```

<br>
<br>

```java
    //Creator<T> 인터페이스 구현
    /**
     * public CREATOR로 구현 및 제공해야 하는 인터페이스
     * Paccel에서 Parcelable 클래스의 인스턴스를 생성하는 필드입니다.
     */
 
    public static final Creator<SimpleData> CREATOR = new Creator<SimpleData>() {
 
        /**
         * 'Parcelable' 클래스의 새 인스턴스를 만들어 인스턴스화합니다.
         * 데이터가 이전에 작성된 적이 있는 지정된 'Parcel'에서
         * {@link Parcelable#writeToParcel Parcelable.Parcel()에 씁니다.
         *
         * @param source 객체의 데이터를 읽을 구획.
         * @Parcelable 클래스의 새 인스턴스를 반환합니다.
         */
 
        @Override
 
        public SimpleData createFromParcel(Parcel parcel) {
 
            Log.d("테스트","\ncreateFromParcel(Parcel parcel){\nReturn new SimpleData(parcel)}");
 
            return new SimpleData(parcel);
 
        }
 
 
 
 
        /**
         * 구획 가능 클래스의 새 배열을 만듭니다.
         *
         * @param size 배열의 크기.
         * @Return 모든 항목이 포함된 구획 가능 클래스의 배열을 반환합니다.
         * null로 초기화되었습니다.
         */
 
        @Override
 
        public SimpleData[] newArray(int size) {
 
            return new SimpleData[size];
 
        }
 
    };
```

<br>
<br>

```java
    /**
     * 수신이 가능한 {@link Creator}의 전문화
     * ClassLoader에서 객체를 생성 중입니다.
     */
 
    public static final ClassLoaderCreator<SimpleData> CLASS_LOADER_CREATOR = new ClassLoaderCreator<SimpleData>() {
 
 
        /**
         * Parcelable 클래스의 새 인스턴스 생성, 인스턴스화
         * 데이터가 이전에 작성된 Parcel의 데이터
         * {@link Parcelable#writeToParcel Parcelable.Parcel()에 쓰기
         * 지정된 ClassLoader를 사용합니다.
         *
         * @param source 객체의 데이터를 읽을 구획.
         * @param loader 이 개체를 만들고 있는 ClassLoader.
         * @Parcelable 클래스의 새 인스턴스를 반환합니다.
         */
        @Override
 
        public SimpleData createFromParcel(Parcel source, ClassLoader loader) {
 
            return null;
 
        }
 
 
 
        @Override
 
        public SimpleData createFromParcel(Parcel source) {
 
            return null;
 
        }
 
 
 
        @Override
 
        public SimpleData[] newArray(int size) {
 
            return new SimpleData[0];
 
        }
 
    };
 
}
```