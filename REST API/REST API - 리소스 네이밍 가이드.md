## REST API - 리소스 네이밍 가이드

<br>

### 1. 마지막에 '/'을 포함하지 않는다.

### Bad

```Java
https://api.test.com/users
```

### Good

```Java
https://api.test.com/users
```

<br>

### 2. \_(underar) 대신 -(dash)을 사용한다.

### Bad

```Java
https://api.test.com/users/post_comments
```

### Good

```Java
https://api.test.com/users/post-comments
```

<br>

### 3. 소문자를 사용한다.

### Bad

```Java
https://api.test.com/users/postComments
```

### Good

```Java
https://api.test.com/users/post-comments
```

<br>

### 4. 행위(method)는 URL에 포함하지 않는다.

### Bad

```Java
https://api.test.com/users/1/delete-post/1
```

### Good

```Java
https://api.test.com/users/1/posts/1
```

<br>

### 5. 서브 리소스로 표현하고, 서브 리소스에 관계 명시한다.

- yoon이라는 사용자가 찜한 상품 목록

### Bad

```Java
https://api.test.com/users/likes/items
```

### Good

```Java
https://api.test.com/users/yoon/likes/items
```

<br>
