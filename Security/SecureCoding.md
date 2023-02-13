https://m.blog.naver.com/dbdudrms95/221948215924


### Public 메소드부터 반환된 Private 배열
private로 선언된 배열을 public으로 선언된 메소드로 반환(return)하면, 그 배열의 레퍼런스가 외부에 공개되어 외부에서 배열수정과 객체 속성변경이 가능해진다

- 대첵


private로 선언된 배열을 public으로 선언된 메소드로 반환하지 않도록 해야 한다. private 배열에
대한 복사본을 반환하도록 하고 배열의 원소에 대해서는 clone() 메소드로 복사된 원소를 저장하도록
하여 private 선언된 배열과 객체속성에 대한 의도하지 않게 수정되는 것을 방지한다. 만약 배열의
원소가 String 타입 등과 같이 변경이 되지 않는 경우에는 Private 배열의 복사본을 만들고 이를 반환하도록 작성한다.

- 코드예제


멤버 변수 colors는 private로 선언되었지만 public으로 선언된 getColors() 메소드로 참조를 얻을
수 있다. 이 경우 의도하지 않은 수정이 발생할 수 있다.
아래의 코드는 멤버 변수 colors는 private로 선언되었지만 public으로 선언된 getUserColors
메소드로 private 배열에 대한 reference를 얻을 수 있다. 이 경우 의도하지 않은 수정이 발생할
수 있다

```
1: // private 인 배열을 public인 메소드가 return한다.
2: private Color[] colors;
3: public Color[] getUserColors(Color[] userColors) { return colors; }
```

private배열에 대한 복사본을 만들고, 복사된 배열의 원소로는 clone() 메소드로 private 배열의 원소
의 복사본을 만들어 저장하여 반환하도록 작성하면, private선언된 배열과 원소에 대한 의도하지 않
은 수정을 방지할 수 있다.


```
1: private Color[] colors;
2: //메소드를 private으로 하거나, 복제본 반환, 수정하는 public 메소드를 별도로 만든다.
3: public void onCreate(Bundle savedInstanceState) {
4: super.onCreate(savedInstanceState);
5: Color[] newColors = getUserColors();
6: ......
7: }
8: public Color[] getUserColors(Color[] userColors) {
9: //배열을 복사한다.
10: Color[] colors = new Color [userColors.length];
11: for (int i = 0; i < colors.length; i++)
12: //clone()메소드를 이용하여 배열의 원소도 복사한다.
13: colors[i] = this.colors[i].clone();
14: return colors;
15:}

```

- 아래의 코드는 멤버 변수 colors는 private로 선언되었지만, public으로 선언된 getColors() 메소드로
reference를 얻을 수 있다. 이 경우 의도하지 않은 배열의 수정이 발생할 수 있다.


```
1: // private 인 배열을 public인 메소드가 return한다.
2: private String[] colors;
3: public String[] getColors() { return colors; }
```

```
1: private String[] colors;
2: // 메소드를 private으로 하거나, 복제본 반환, 수정하는 public 메소드를 별도로 만든다.
3: public void onCreate(Bundle savedInstanceState) {
4: super.onCreate(savedInstanceState);
5: String[] newColors = getColors();
6: ......
7: }
8: public String[] getColors() {
9: String[] ret = null;
10: if ( this.colors != null ) {
11: ret = new String[colors.length];
12: for (int i = 0; i < colors.length; i++) { ret[i] = this.colors[i]; }
13: }
14: return ret;
15: }

```


###  Private 배열에 Public 데이터 할당
public으로 선언된 메소드의 인자가 private선언된 배열에 저장되면, private배열을 외부에서 접근
하여 배열수정과 객체 속성변경이 가능해진다.


#### 보안대책
public으로 선언된 메서드의 인자를 private선언된 배열로 저장되지 않도록 한다. 인자로 들어온
배열의 복사본을 생성하고 clone() 메소드로 복사된 원소를 저장하도록 하여 private변수에 할당
하여 private선언된 배열과 객체속성에 대한 의도하지 않게 수정되는 것을 방지한다. 만약 배열 객체
의 원소가 String 타입 등과 같이 변경이 되지 않는 경우에는 인자로 들어온 배열의 복사본을 생성
하여 할당한다.

- 아래의 코드는 멤버 변수 userRoles는 private로 선언되었지만 public으로 선언된 setUserRoles
메소드로 인자가 할당되어 배열의 원소를 외부에서 변경할 수 있다. 이 경우 의도하지 않은 배열과
원소에 대한 객체속성 수정이 발생할 수 있다.

```
1: //userRoles 필드는 private이지만, public인 setUserRoles()로 외부의 배열이 할당되면, 사실상
public 필드가 된다.
2: private UserRole[] userRoles;
3: public void setUserRoles(UserRole[] userRoles) {
4: this.userRoles = userRoles;
5: }
```

인자로 들어온 배열의 복사본을 생성하고 clone() 메소드로 복사된 원소를 저장하도록 하여 private
변수에 할당하면 private으로 할당된 배열과 원소에 대한 의도하지 않은 수정을 방지할 수 있다.
```
1: //객체가 클래스의 private member를 수정하지 않도록 한다.
2: private UserRole[] userRoles;
3: public void setUserRoles(UserRole[] userRoles) {
4: this.userRoles = new UserRole[userRoles.length];
5: for (int i = 0; i < userRoles.length; ++i)
6: this.userRoles[i] = userRoles[i].clone();
7: }
```

- 아래의 코드는 멤버 변수 userRoles는 private로 선언되었지만 public으로 선언된 setUserRoles
메소드로 인자가 할당되어 배열의 원소를 외부에서 변경할 수 있다. 이 경우 의도하지 않은 배열에
대한 수정이 발생할 수 있다.

```
1: //userRoles 필드는 private이지만, public인 setUserRoles()로 외부의 배열이 할당되면, 사실상
public 필드가 된다.
2: private String[] userRoles;
3: public void setUserRoles(String[] userRoles) {
4: this.userRoles = userRoles;
5: }
```
인자로 들어온 배열의 복사본을 생성하여 private변수에 할당하면 private으로 할당된 배열에 대한
의도하지 않은 수정을 수 있다.

```
1: //객체가 클래스의 private member를 수정하지 않도록 한다.
2: private String[] userRoles;
3: public void setUserRoles(String[] userRoles) {
4: this.userRoles = new String[userRoles.length];
5: for (int i = 0; i < userRoles.length; ++i)
6: this.userRoles[i] = userRoles[i];
7: }
```



