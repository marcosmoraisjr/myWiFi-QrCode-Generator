# Gerador de QR Code para Wi-Fi

Este é um projeto que consiste em um gerador de QR Code para configurações de Wi-Fi. Com ele, você pode facilmente gerar um QR Code contendo as informações necessárias para conectar-se a uma rede Wi-Fi, como o nome da rede (SSID), tipo de segurança e senha.

## Como usar

1. **Preencha as informações**: No formulário fornecido, preencha o nome da rede (SSID) e selecione o tipo de segurança (WPA/WPA2, WEP ou sem senha).
2. **Senha sugerida**: Ao preencher o campo SSID, uma senha sugerida será automaticamente gerada, baseada no nome da rede. Você pode usar essa senha sugerida ou inserir uma senha personalizada.
3. **Gerar QR Code**: Clique no botão "Gerar QR Code" para criar o código QR com as informações fornecidas.
4. **Conectar-se à rede**: Use um leitor de QR Code em seu dispositivo para escanear o código gerado e conectar-se à rede Wi-Fi automaticamente.

## Recursos e Tecnologias

- **HTML, CSS e JavaScript**: O projeto é desenvolvido utilizando tecnologias web padrão.
- **Biblioteca qrcode-generator**: Utilizada para gerar o código QR de forma dinâmica.
- **Bootstrap**: Framework CSS utilizado para estilização e responsividade.

## Importante
As funções mais importantes são descritas abaixo:

- Função para alternar a visibilidade da senha
```bash
        function togglePasswordVisibility() {
            var passwordField = document.getElementById('password');
            var toggleButton = document.querySelector('.btn-outline-secondary');
            if (passwordField.type === "password") {
                passwordField.type = "text";
                toggleButton.textContent = "👁️";
            } else {
                passwordField.type = "password";
                toggleButton.textContent = "🔒";
            }
        }
```
- Função para gerar a senha sugerida
```javascript
        function generateSuggestedPassword() {
            var suggestedPassword = "";
            var password = document.getElementById('password');
            var security = document.getElementById('security').value;

            // Verifica o tipo de segurança e gera a senha sugerida conforme os critérios
            if (security === "WPA") {
                var ssid = document.getElementById('ssid').value.toLowerCase();
                var characters = "aeiou_";
                var replacements = "4310v@$";

                for (var i = 0; i < ssid.length; i++) {
                    var char = ssid.charAt(i);
                    var index = characters.indexOf(char.toLowerCase());
                    suggestedPassword += index !== -1 ? replacements[index] : char;
                }
            } else if (security === "WEP") {
                // Implemente a lógica para WEP, se necessário
            } else if (security === "nopass") {
                // Implemente a lógica para redes sem senha, se necessário
            }

            return suggestedPassword;
        }
```

- Função para preencher o campo de senha com a sugestão calculada ao sair do campo SSID
```javascript
        function fillPasswordField() {
            var suggestedPassword = generateSuggestedPassword();
            var passwordField = document.getElementById('password');
            passwordField.value = suggestedPassword;
        }
```

- Função para gerar o QR Code
```javascript
       function generateQRCode() {
            var ssid = document.getElementById('ssid').value.trim();
            var security = document.getElementById('security').value;
            var password = document.getElementById('password').value.trim();
            var hidden = document.getElementById('hidden').checked;

            // Restante do seu código para gerar o QR Code
            // Construção dos dados para o QR Code
            var wifiData = `WIFI:S:${ssid};T:${security};P:${password};${hidden ? 'H:true;' : ''};`;

            // Configuração do QR Code
            var typeNumber = 4;
            var errorCorrectionLevel = 'L';
            var qr = qrcode(typeNumber, errorCorrectionLevel);
            qr.addData(wifiData);
            qr.make();

            // Exibição do QR Code
            document.getElementById('qrcode').innerHTML = qr.createImgTag(6); // Alterado o parâmetro de tamanho para 5

            // Mostrar a caixa flutuante
            document.getElementById('qrcodeContainer').style.display = 'block';
```

- Função para fechar o QR Code - gerado
```javascript
       function closeQRCode() {
            // Ocultar a caixa flutuante
            document.getElementById('qrcodeContainer').style.display = 'none';
        }
```

## Instalação

Na sessão <head> do seu código HTML insira:

```bash
<script src="https://cdn.jsdelivr.net/npm/qrcode@1.5.3/lib/browser.min.js"></script>
```
ou se preferir..

### QRCode / API de Código de Barras 2D

[![Version](https://img.shields.io/badge/version-1.5.3-brightgreen)](https://github.com/soldair/node-qrcode/releases/tag/v1.5.3)

[![License](https://img.shields.io/badge/license-MIT-blue)](https://github.com/soldair/node-qrcode/blob/master/LICENSE)

Este é um repositório contendo uma API para geração de códigos QR (Quick Response) e códigos de barras 2D. A API oferece suporte tanto no lado do servidor quanto no lado do cliente, usando canvas para renderização.

## Como usar

```bash
<script src="https://cdn.jsdelivr.net/npm/qrcode@1.5.3/lib/browser.min.js"></script>
```

#### Destaques

- Funciona no servidor e no cliente (incluindo React Native com SVG)
- Utilitário de linha de comando (CLI)
- Geração de código QR em formato de imagem
- Suporte para Modo Numérico, Alfanumérico, Kanji e Byte
- Suporte para modos mistos
- Suporte para caracteres chineses, cirílicos, gregos e japoneses
- Suporte para caracteres multibyte (como emojis 😊)
- Gera automaticamente segmentos otimizados para melhor compressão de dados e menor tamanho de código QR
- Leitura agnóstica de aplicativos, os códigos QR são, por definição, agnósticos de aplicativos

#### Uso

#### API

Para mais detalhes sobre como usar a API, consulte [a documentação completa](https://github.com/soldair/node-qrcode).

#### Licença

Este projeto está licenciado sob a [Licença MIT](https://github.com/soldair/node-qrcode/blob/master/LICENSE).

*A palavra "QR Code" é uma marca registrada da DENSO WAVE INCORPORATED.*

## Como contribuir

Este projeto está aberto para contribuições. Se você encontrar algum problema ou tiver sugestões de melhorias, sinta-se à vontade para abrir uma issue ou enviar um pull request.
