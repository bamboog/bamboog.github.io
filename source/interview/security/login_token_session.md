####  登录
- session   网页
  - redis

- token     app
  - JWT(JSON Web Tokens)
    - 用加密算法和指定密钥对认证信息（用户账号）进行运算后，生成的一串字符串
    -
    ```java
    public String generateToken(User user) {
      Map<String, Object> claims = new HashMap<>();
      claims.put(CLAIM_KEY_USERNAME, user.getUsername());
      claims.put(CLAIM_KEY_CREATED, new Date());
      return generateToken(claims);
    }

    String generateToken(Map<String, Object> claims) {
        return Jwts.builder()
                .setClaims(claims)
                .setExpiration(generateExpirationDate()) //设置Token的 有效期；
                .signWith(SignatureAlgorithm.HS512, secret) // secret 就是加密的密钥
                .compact();
    }
    ```
  - OAuth

  - 怎么设计

  - SpringSecurity  --- 过滤那些url需要鉴权
