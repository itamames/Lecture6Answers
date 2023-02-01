# Lecture6Answers
1. 

```java
public class ArrayStack2<E> implements LIFOStack<E> {

	// Implementation of a stack using an array
	// with the top of the stack in position 0 always
	// (not a very efficient way of doing things, of course)

	private E[] dataArray;
	private int bottom;

	public ArrayStack2() {
		dataArray = (E[])new Object[1];
		bottom = -1;
	}
	
	public void push(E element) {
		if (bottom == dataArray.length-1)
			reallocate();
		for (int i = bottom; i >= 0; i--)
			dataArray[i+1] = dataArray[i];
		dataArray[0] = element;		// top is always at index 0
		bottom++;
	}
	
	public boolean isEmpty() {
		return bottom == -1;
	}

	public E pop() {
		if (isEmpty())
			throw new NoSuchElementException();
		E result = dataArray[0];
		for (int i = 1; i <= bottom; i++)
			dataArray[i-1] = dataArray[i];
		bottom--;
		return result;		
	}
		
	public E peek() {
		if (isEmpty())
			throw new NoSuchElementException();
		return dataArray[0];
	}
	
	private void reallocate() {
		E[] newArray = (E[]) new Object[dataArray.length*2];
		System.arraycopy(dataArray, 0, newArray,0,dataArray.length);
		dataArray = newArray;
	}
}
```

2.
```java
public class Calculator {
	public static void main(String[] args) {
		Scanner scan = new Scanner(System.in);
		InfixToPostfixGenerator generator = new InfixToPostfixGenerator();
		PostfixEvaluator evaluator = new PostfixEvaluator();
		try {
			System.out.println("Input infix expression: ");
			String infix = scan.nextLine();
			String postfix = generator.convert(infix);
			int value = evaluator.eval(postfix);
			System.out.println("Value = " + value);
		}
		catch (SyntaxErrorException e) {
			System.out.println("Error. Conversion terminated.");
			System.out.println(e.getMessage());
		}
	}
}
```
