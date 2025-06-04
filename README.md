<img src="https://capsule-render.vercel.app/api?type=waving&color=ff79c6&height=100&section=footer"/>

# TDD 🌸 FEMMCode 🌸
Essa parte do tdd foi feito com o que foi desenvolvido na spint 1-login e cadasto 

✨ Passo 1 — Criando os testes primeiro
Crie uma classe de teste chamada AuthTest.java, por exemplo dentro do pacote tests ou na pasta padrão de testes.


```
import static org.junit.jupiter.api.Assertions.assertEquals;
import org.junit.jupiter.api.Test;
public class AuthTest {

    @Test
    public void testLoginSucesso() {
        String resultado = Auth.login("usuario@teste.com", "1234");
        assertEquals("Login efetuado com sucesso", resultado);
    }

    @Test
    public void testLoginEmailInvalido() {
        String resultado = Auth.login("emailinvalido", "1234");
        assertEquals("Email inválido", resultado);
    }

    @Test
    public void testLoginSenhaIncorreta() {
        String resultado = Auth.login("usuario@teste.com", "senhaerrada");
        assertEquals("Senha incorreta", resultado);
    }

    @Test
    public void testLoginUsuarioNaoCadastrado() {
        String resultado = Auth.login("naoexiste@teste.com", "1234");
        assertEquals("Usuário não encontrado", resultado);
    }

    @Test
    public void testLoginCamposVazios() {
        String resultado = Auth.login("", "");
        assertEquals("Preencha todos os campos", resultado);
    }
```
✨Passo 2 — Construindo a classe Auth.java
```
import java.util.HashMap;
import java.util.Map;
import java.util.regex.Pattern;

public class Auth {

    // Simulando um banco de dados de usuários
    private static Map<String, String> usuarios = new HashMap<>();

    static {
        usuarios.put("usuario@teste.com", "1234");
    }

    private static boolean validarEmail(String email) {
        String padrao = "^[\\w.-]+@[\\w.-]+\\.\\w+$";
        return Pattern.matches(padrao, email);
    }

    public static String login(String email, String senha) {
        if (email == null || email.isEmpty() || senha == null || senha.isEmpty()) {
            return "Preencha todos os campos";
        }

        if (!validarEmail(email)) {
            return "Email inválido";
        }

        if (!usuarios.containsKey(email)) {
            return "Usuário não encontrado";
        }

        if (!usuarios.get(email).equals(senha)) {
            return "Senha incorreta";
        }

        return "Login efetuado com sucesso";
    }
```

✨Passo 3 — Executando os testes
Certifique-se de que seu projeto esteja configurado para usar JUnit 5.

No Maven, adicione no pom.xml:
```

<dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter</artifactId>
    <version>5.10.0</version>
    <scope>test</scope>
</dependency>
```

Rode os testes via IDE (IntelliJ, Eclipse) ou via linha de comando:
```
mvn test
```
ou se estiver usando Gradle:
```
./gradlew test
```
<img src="https://capsule-render.vercel.app/api?type=waving&color=ff79c6&height=100&section=footer"/>
