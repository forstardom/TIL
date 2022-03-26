### 1. URL Rules

### 1.1 마지막에 '/'을 포함하지 않는다.

### Bad

```Java
https://api.test.com/users
```

### Good

```Java
https://api.test.com/users
```

<br>

### 1.2 \_(underar) 대신 -(hyphen)을 사용한다.

### Bad

```Java
https://api.test.com/users/post_comments
```

### Good

```Java
https://api.test.com/users/post-comments
```

<br>

### 1.3 소문자를 사용한다.

### Bad

```Java
https://api.test.com/users/postComments
```

### Good

```Java
https://api.test.com/users/post-comments
```

<br>

### 1.4 행위(method)는 URL에 포함하지 않는다.

### Bad

```Java
https://api.test.com/users/1/delete-post/1
```

### Good

```Java
https://api.test.com/users/1/posts/1
```

<br>
