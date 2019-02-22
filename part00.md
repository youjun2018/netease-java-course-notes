```Java
import java.math.BigDecimal;

public class Main {

	public static void main(String[] args) {
		float g = 0.7f - 0.6f;
		float h = 0.8f - 0.7f;
		System.out.println(g);
		System.out.println(h);
		if(g == h)
		{
			System.out.println("true");
		}
		else
		{
			System.out.println("false");
		}

		Float x = Float.valueOf(g);
		Float y = Float.valueOf(h);
		System.out.println(x);
		System.out.println(y);
		if(x.equals(y))
		{
			System.out.println("true");
		}
		else
		{
			System.out.println("false");
		}

		BigDecimal m = new BigDecimal(0.7);
		BigDecimal n = new BigDecimal("0.7");
		System.out.println(m);
		System.out.println(n);
		if(m.equals(n))
		{
			System.out.println("true");
		}
		else
		{
			System.out.println("false");
		}
	}
}
```
结果：
```
0.099999964
0.100000024
false
0.099999964
0.100000024
false
0.6999999999999999555910790149937383830547332763671875
0.7
false
```
