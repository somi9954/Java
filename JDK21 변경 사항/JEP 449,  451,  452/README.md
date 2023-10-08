# JEP 449: Deprecate the Windows 32-bit x86 Port for Removal

* 이후 릴리스에서 Windows 32bit x86 port를 제거하기 위해, 이를 Deprecate 시켰다. 이제 Windows 32bit 용 빌드를 구성하려고 시도할 때 오류 메세지가 표시된다.

```JAVA
$ bash ./configure
...
checking compilation type... native
configure: error: The Windows 32-bit x86 port is deprecated and may be removed in a future release. \\
Use --enable-deprecated-ports=yes to suppress this error.
configure exiting with result code 1
$
```

# JEP 451: Prepare to Disallow the Dynamic Loading of Agents 
* 자바는 agent를 통해 애플리케이션 코드를 동적으로 변경하도록 지원해왔고, 이를 통해 애플리케이션을 모니터링하고 관찰하는 많은 방법들이 탄생하게 되었다. 대표적으로 Pinpoint와 같은 도구는 자바 에이전트를 기반으로 바이트 코드를 조작하여 모니터링을 돕는 APM 도구이다.
* 이러한 자바 애플리케이션을 프로파일링하는 정상적인 방법들은 애플리케이션이 실행될 때 불러와지고, 애플리케이션이 실행되는 중간에 불러와지는 경우가 거의 없다. 따라서 자바 21에서는 실행 중인 JVM에 에이전트가 동적으로 로드될 때 경고를 발행시키도록 수정되었다. 물론 JVM 시작 시에 에이전트를 로드하는 것은 경고를 발생시키지 않는다.

# JEP 452: Key Encapsulation Mechanism API 
* Java21에는 공개 키 암호화를 사용하여 대칭 키를 보호하는 암호화 기술인 KEM(Key Encapsulation Mechanism) API가 도입되었다. 기존의 기술은 무작위로 생성된 대칭 키를 공개 키로 암호화하는 것이지만, 패딩이 필요하고 보안을 증명하기 어려울 수 있다. 대신 KEM은 공개 키의 속성을 사용하여 패딩이 필요 없는 관련 대칭 키를 도출한다.
* KEM은 양자 공격을 방어하기 위한 핵심 도구가 될 것이다. 다른 보안 제공업체들은 이미 표준 KEM API에 대한 필요성을 표명했고, 자바 역시 이를 공식적으로 도입하기로 결정하였다.

```JAVA
package javax.crypto;

public class DecapsulateException extends GeneralSecurityException;

public final class KEM {

    public static KEM getInstance(String alg)
        throws NoSuchAlgorithmException;
    public static KEM getInstance(String alg, Provider p)
        throws NoSuchAlgorithmException;
    public static KEM getInstance(String alg, String p)
        throws NoSuchAlgorithmException, NoSuchProviderException;

    public static final class Encapsulated {
        public Encapsulated(SecretKey key, byte[] encapsulation, byte[] params);
        public SecretKey key();
        public byte[] encapsulation();
        public byte[] params();
    }

    public static final class Encapsulator {
        String providerName();
        int secretSize();           // Size of the shared secret
        int encapsulationSize();    // Size of the key encapsulation message
        Encapsulated encapsulate();
        Encapsulated encapsulate(int from, int to, String algorithm);
    }

    public Encapsulator newEncapsulator(PublicKey pk)
            throws InvalidKeyException;
    public Encapsulator newEncapsulator(PublicKey pk, SecureRandom sr)
            throws InvalidKeyException;
    public Encapsulator newEncapsulator(PublicKey pk, AlgorithmParameterSpec spec,
                                        SecureRandom sr)
            throws InvalidAlgorithmParameterException, InvalidKeyException;

    public static final class Decapsulator {
        String providerName();
        int secretSize();           // Size of the shared secret
        int encapsulationSize();    // Size of the key encapsulation message
        SecretKey decapsulate(byte[] encapsulation) throws DecapsulateException;
        SecretKey decapsulate(byte[] encapsulation, int from, int to,
                              String algorithm)
                throws DecapsulateException;
    }

    public Decapsulator newDecapsulator(PrivateKey sk)
            throws InvalidKeyException;
    public Decapsulator newDecapsulator(PrivateKey sk, AlgorithmParameterSpec spec)
            throws InvalidAlgorithmParameterException, InvalidKeyException;

}
```

----
출처 : https://mangkyu.tistory.com/308 </br>
출처 : https://openjdk.org/jeps/449 </br>
출처 : https://openjdk.org/jeps/451 </br>
출처 : https://openjdk.org/jeps/452 </br>

 
