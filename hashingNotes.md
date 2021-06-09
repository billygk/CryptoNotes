Notes on hashing in particular SHA256 & SHA512

```
Hashes are generally expressed in hexadecimal strings like:

                 1         2         3         4         5         6   
        1234567890123456789012345678901234567890123456789012345678901234
sha256: c4d8e1c781c74cbdb11986965b42c109bd6f67875afd22fec0dea2a1a7546561
length: 64

                 1         2         3         4         5         6         7         8         9         10        11        12  
        12345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678
sha512: 5d545722a91a88f6247b929363aa69fec7882fd79fd6d9fe532aaa714f35a18e0a3566ca3536708c778567fa7d481824f2b732e6d6f20c4d2496d22f23dffbbb
length: 128
```


Zincs implementation:
```
public String getSha256(String input) {
  try {
    MessageDigest digest = MessageDigest.getInstance("SHA-256");
    digest.reset();
    digest.update(input.getBytes(StandardCharsets.UTF_8));
    return String.format("%064x", new BigInteger(1, digest.digest()));
  } catch (Exception e) {
    e.printStackTrace();
  }
  return null;
}
```

Apache Common Codec:
```
String sha256hex = org.apache.commons.codec.digest.DigestUtils.sha256Hex(stringText);   
```

Guava Hashing:
```
final String hashed = Hashing.sha256().hashString("your input", StandardCharsets.UTF_8).toString();
```

Using Java 8 byte[]:
```
MessageDigest digest = MessageDigest.getInstance("SHA-256");
byte[] hash = digest.digest(text.getBytes(StandardCharsets.UTF_8));
String encoded = Base64.getEncoder().encodeToString(hash);
```

Java MessageDigest available algorithms: 
https://docs.oracle.com/javase/8/docs/technotes/guides/security/StandardNames.html#MessageDigest

source:
https://stackoverflow.com/questions/5531455/how-to-hash-some-string-with-sha256-in-java

