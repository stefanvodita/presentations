Topic: 32 bit floating point ieee 754 java


Interactive true or false statement of varying difficulty.
If you get them all right, come talk to me after so I can personally congratulate you.


0. I can cast a 32 bit integer to a float without precision loss - false; common operation when wanting float division of integers


1. If a, b, c consecutive, equidistance - false, floats are more dense around 0


2. a+b=b+a true, except NaN != NaN


3. a+b can equal a with b not 0 true, story about Lucene geospatial, circle with center at large coordinates radius collapsed to 0 ends up a point


4. a+b+c=c+b+a  false, story about aggregations, Kahan summation


We could go on, but stop there.
Don't trust floats!



Code:
```
class FloatCastToInt {
    public static void main(String[] args) {
        int x = Integer.MAX_VALUE;
        int y = 2;
        float z = (float) x / y;
        
        System.out.println(x);
        System.out.println((float) x);
        System.out.println((double) x);
        System.out.println((float) x / y);
        System.out.println((double) x / y);
    }
}
```
```
class FloatsAreEquidistant {
    public static void main(String[] args) {
        float y = 8f;
        float x = Math.nextDown(y);
        float z = Math.nextUp(y);
        
        System.out.println(x);
        System.out.println(y);
        System.out.println(z);
        System.out.println(y-x);
        System.out.println(z-y);
    }
}
```
```
class FloatSumIsNotCommutative {
    public static void main(String[] args) {
        float x = 177182.61f;
        float acc;
        
        acc = 0;
        acc += x;
        acc += Float.NaN;
        System.out.println(acc);
        System.out.println(acc == Float.NaN);
        
        acc = 0;
        acc += Float.NaN;
        acc += x;
        System.out.println(acc);
        System.out.println(acc == Float.NaN);
    }
}
```
```
class FloatSumHasMultipleIdentityElements {
    public static void main(String[] args) {
        float x = (float) 1e-4;
        float y = (float) 1e4;
        float acc;
        
        acc = 0;
        acc += x;
        acc += y;
        System.out.println(acc);
        System.out.println(acc == x);
        System.out.println(acc == y);
    }
}
```
```
class FloatSumIsNotAssociative {
    public static void main(String[] args) {
        float x = 177182.61f;
        float y = 238089.27f;
        float z = 255214.66f;
        float acc;
        
        acc = 0;
        acc += x;
        acc += y;
        acc += z;
        System.out.println(acc);
        
        acc = 0;
        acc += x;
        acc += (y + z);
        System.out.println(acc);
        
        acc = 0;
        acc += z;
        acc += y;
        acc += x;
        System.out.println(acc);
    }
}
```
