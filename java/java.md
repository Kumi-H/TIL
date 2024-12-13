## Java

### 環境構築

▼x64 Installerをダウンロード<br>
https://www.oracle.com/jp/java/technologies/downloads/#jdk23-windows

▼パスを通す方法（参考にしたページ）<br>
https://www.techfun.co.jp/services/magazine/java/windows-jdk-pathset.html

▼VS Codeの設定（参考にしたページ）<br>
https://note.com/liber_grp/n/n88f3f0a6fdf1

---

### オブジェクト指向とは
**処理を部品化して、部品を組み合わせることで1つのプログラムを作る考え方**

```markdown
オブジェクト指向の3原則
・継承
・ポリモーフィズム（多態性）
・カプセル化
```

---

### パッケージ

- 名前空間を提供し、名前の衝突を避ける
- アクセス修飾子と組み合わせてアクセス制御機能を提供する
- クラスの分類を可能にする
- パッケージを省略したクラスはデフォルトで無名パッケージに属する

```java
package sample;  // 必ず先頭行に記述
import aaa;

public class Sample{

}

```

---

### 出力

```java
System.out.println("Hello World");  // println -> プリントラインと読む

// 改行せずに値を出力する場合
System.out.print("出力: ");
```

---

### コマンド
#### javaコマンド
```java
java Sample.java
```

#### javacコマンド
```java
javac Sample.java  // コンパイル
java Sample        // 実行
```



---

### エントリーポイント

処理を始めるためのメソッドのこと

```java
public static void main(String[] args){
	// 処理
}
```

**条件**
- `public`であること
- インスタンスを生成しなくても実行できること（`static`であること）
- 戻り値は戻せないこと（`void`であること）
- メソッド名は`main`であること
- 引数は配列`String[]`のほかに、可変長のString型`String…`を受け取ることもできる

---

### データ型

#### プリミティブ型
* プリミティブ型の変数はデータそのものを保持している

|データ型|説明|
|-------|----|
|boolean|    |
|char|String型の変数には代入できない。シングルクォーテーションで括るとchar型として扱われる。
|byte|整数 -128~127
|short|整数 -32768~32767
|int|整数
|long|整数 lかLを末尾につける
|float|小数点 1.99fのようにfかFを末尾につける
|double|小数点

#### 参照型
* オブジェクトへの参照（リンク）を保持している。
* 参照を保持していない場合のリテラルは`null`

#### 整数メモ
* 2進数: 0bで始まる
* 8進数: 0から始まる
* 16進数: 0Xで始まる
* 整数リテラルでのアンダースコアのルール
	* リテラルの先頭と末尾には使用できない
	* 記号の前後には使用できない（記号: ドット, L, F, 0b, 0X） 

#### StringBuilder
* デフォルトで16文字バッファを持っている

---
### 比較
#### 同一・同値・同種

同一: ==演算子を使う　（参照が同じかどうか）

同値: equalsメソッドを使う

同種: instanceof演算子を使う（型の互換性があるか）

* ==演算子でインスタンスを作る場合は、定数用のメモリ空間に作られる
* new演算子でインスタンスを作る場合は、インスタンス用のメモリ空間に作られる
* equalsメソッドは引数にnullを渡されるとfalseを返す

---

### 変数・定数

#### 定数の宣言

```java
final String GREETING_MSG = "こんにちは、世界！";
```
- 先頭にfinalを付与する
- 型を指定
- 定数名はすべて大文字のアンダースコア形式で命名する

#### 変数名
* キャメルケースで記述する

#### var
* ローカル変数の宣言のみに使用できる
* フィールドの宣言には使用できない
* 引数の型宣言には使用できない
* ラムダ式を受け取る変数宣言には使用できない
* 配列の宣言には使用できない

---

### 配列

**配列の宣言**

```java
int[] 変数名;
int 変数名[];  // 大カッコは変数名の後ろでもOK

// 二次元配列
int[][] arrayA;
int[] arrayA[];

// 三次元配列
int arrayB[][][];
int[][] arrayB[];
```

**配列インスタンスの生成**

```java
int[] array = new int[3]; // 要素数3つの配列

// 以下2つは同じ意味(要素数ゼロ。これは実行するとハッシュコードが返る)
int[] array = {};
int[] array = new int[0];

// 以下2つは同じ意味
int[] array = {1, 2};
int[] array = new int[]{1, 2};　
// ↑初期化子{}を使う場合は、new int[]の大カッコ内に要素数は書かない（自動的に要素数が決まるため）

int[][] array = new int[][]{};
int[][] array = {}; // 初期化子が自動的に必要な次元数を算出するのでOK
```

※初期化子は変数宣言と同時にしか使えない


---

### ArrayList

ジェネリクスの指定なしのArrayListインスタンス

```java
ArrayList list = new ArrayList();

ArrayList list = new ArrayList<>();
```

型が混在しないようにするにはジェネリクスを使う

```java
ArrayList<String> list = new ArrayList<>();
```

固定長のリストを作る方法

```java
// Listインターフェースのofメソッドを使う
var list = List.of(1, 2, 3);

// ArraysクラスのasListクラスを使う
var list = Arrays.asList(new Integer[]{1, 2, 3});

Integer[] array = {1, 2, 3};
var list = Arrays.asList(array);
```

**removeメソッド**<br>
条件が合致する最初の要素を削除する


---

### switch文、switch式

**switch文**
* breakを入れないとフォールスルーする
* defaultはなくてもよい。

**switch式（Java SE 14以降から使える）**
*  `->` を使う
* break不要
* defaultは欠かせない（位置はどこでもよい）
* 文の終わりにセミコロンが必要
* 値を戻すにはyieldを使う

---

### 繰り返し

#### do-while文
* 中カッコを省略した場合、doとwhileの間は1文のみ記述できる
* 2文以上記述した場合はコンパイルエラーとなる

#### 拡張For文
* 配列の場合に使える

```java
for (String name: names) // name->配列の要素, names->配列
```

---
### クラス
```java
class Sample{

}
```
**クラスフィールド**  

- 初期値も設定できる

```java
public static String name;
public static データ型 変数名;
```

**クラスメソッド**

- クラスメソッドはインスタンスを生成しない状態でも呼び出すことができる

```java
public static 戻り値の型 メソッド名();
```


---
### コンストラクタ・初期化子

#### コンストラクタ

- newを使ってインスタンスを生成した後に自動で呼び出される特別なメソッド
- コンストラクタ名はクラス名と同じにする
- 戻り値を書いてはいけない（voidも書かない）
- アクセス修飾子に制限はない

```java
class Person {
	Person(){
	
	}
}
```

#### 初期化子

- コンストラクタを複数定義していた場合、すべてのコンストラクタで共通する処理がある場合に使用
- インスタンスを生成するタイミングで実行される
- コンストラクタが実行される前に実行される

```java
public class Sample{
	{
		// 共通の前処理
	}
}
```

※コンストラクタと初期化子は、インスタンスを生成するタイミングでしか実行されない<br>
インスタンスを生成せずにクラス変数を初期化したい場合はstatic初期化子を使う

#### static初期化子

- クラスがロードされたタイミングで実行される

```java
public class Sample{
	static{
	}
}
```

---
### this

* 2つの用途がある。

1. オーバーロードされた別のコンストラクタを呼び出すときに使うthis
	* 最初に記述すること（下記の場合、this("Hello");の前に処理は記述できない。記述するとコンパイルエラーになる） 

```java
public class Sample{
	public Sample(){
		this("Hello"); // public Sample(String str)を呼び出している
	}
	
	public Sample(String str){
		System.out.println(str);
	}
}
```

2. インスタンスそのものを表す参照を入れる特別な変数として使うthis

```java
public class Sample{
	private String value;
	public Sample(String value){
		this.value = value;
	}
}
```

---

### メソッド
* クラスの中で使える

```java
戻り値が無い場合
public static void メソッド名(){
}

戻り値が文字列型の場合
public static String メソッド名(){
	return 戻り値;
}
```

#### ゲッター

- フィールドの値を返すだけのメソッド
- `getフィールド名`のように命名するのが一般的

#### セッター

- フィールドの値を変更するメソッド
- `setフィールド名`のように命名するのが一般的
- 戻り値はない

---
#### オーバーロード
- クラスの中で同名のメソッドやコンストラクタを定義すること
- 成立する条件: 引数の数や型、順番が異なること

#### オーバーライド
- スーパークラスから継承したメソッドと同名のメソッドをサブクラスに定義し、スーパークラスのメソッドの内容を上書きすること
- 戻り値型は、元の定義と同じ型か、サブクラス型であること
- アクセス修飾子は、元の定義と同じか、より緩いものしか指定できない
```java
class Super {
	public void Sample(){
	}
}
```

```java
class Child extends Super {
	public void Sample(){
		// スーパークラスのSampleメソッドがpublicで修飾されているので
		// より厳しい制限となるprivateで修飾はできない
	}
}
```



---
### レコード
- 名前付きタプル
- 一度保持したデータは変更できない
- 継承できない（サブクラスを作れない）
```java
アクセス修飾子 record Customer (String name, int age, String address){
}
```


---
### インスタンス
* オブジェクトの別名であり、実体という意味
* 実際の開発でも、インスタンスにどんな情報を持たせるかをまず考え、書き出したりする


**インスタンスフィールド**

```java
public String name;
public データ型 変数名;
```

**インスタンスメソッド**

```java
public 戻り値の型 メソッド名();
```

---

**カプセル化**

説明入れる

private クラス内からはアクセス可。

protected: クラス内とサブクラスからのみアクセス可。



**継承**

- 既存のクラスのフィールドやメソッドを別のクラスに引き継ぐ機能
- スーパークラス: 継承されるクラス
- サブクラス: 継承してできる新しいクラス
- サブクラスはスーパークラスのメソッドを呼び出せる
- スーパークラスはサブクラスのメソッドを呼び出すことはできない

スーパークラス

```java
class スーパークラス名{
}
```

サブクラス

```java
class サブクラス名 extends スーパークラス名{
}
```

サブクラスからスーパークラスのコンストラクタを呼び出す場合

```java
class Car extends Vehicle{
	Car(){
		super(); 　// ←これでVehicleクラスのコンストラクタが呼び出せる
	}
}
```

#### 抽象メソッド・抽象クラス

- サブクラス（具象クラス）が抽象メソッドをオーバーライドしていなければエラーになる
- サブクラスに、あるメソッドを必ず持たせたいという場合は、スーパークラスに抽象メソッドとして定義しておくことが大事
- 抽象メソッドを1つでも持つクラスは「抽象クラス」と呼ばれる
- 抽象クラスはクラス名の前に`abstract`をつける必要がある
- 抽象クラスはインスタンスを生成できない

```java
abstract class Vehicle {
	
	public abstract void run(int distance); // 処理は書かない！
}
```

**多態性　ポリモーフィズム**


---
### インターフェース

- インターフェースはインスタンス化できない
- 定数（※）、デフォルトメソッド、クラスメソッド（staticで修飾されたメソッド）以外の実装は記述できない<br>
※インタフェースのメンバ変数は自動的にpublic static finalが付けられるため定数になる
- インターフェースを実現するクラスを作りインスタンス化する
- 多重継承することができる

```java
// インターフェースの宣言
interface インターフェース名{
}
```

```java
// インターフェースの実現
class クラス名 implements インターフェース名{
}

// 複数のインターフェースを実現する場合
class クラス名 implements インターフェースA, インターフェースB{
}
```

----
### シールクラス
- Java SE 17から導入

```java
// permitsの後に継承を許可するクラスを指定
public sealed class スーパークラス名 permits A, B{

}
```

---
### 例外処理

**チェック例外**<br>
Exception 例外処理を記述したかどうかをコンパイラが検査する例外

**非チェック例外**<br>
RuntimeException 例外処理を記述したかどうかをコンパイラが検査しない例外

---
### memo
**JVM**<br>
Java仮想マシン