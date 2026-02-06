### Video Demo Tutorial: https://www.youtube.com/watch?v=RG-dclLtYvA

# WhatsAppScripts TravaZap

- [Overview](#overview)
- [Prerequisites](#prerequisites)
- [Usage](#usage)
- [Parameters](#parameters)
- [Error Handling](#error-handling)
- [Example](#example)

## Overview

The `enviarScript` function is an asynchronous JavaScript function designed to send a series of messages to a conversation on a web page. It splits the provided script text into lines, simulates user input by typing each line into the conversation textarea, and then clicks the send button to dispatch the messages.

## Prerequisites

REQUIREMENT: WhatsApp Web Version
https://web.whatsapp.com/

Before using the `enviarScript` function, ensure the following:

- The script is executed in an environment with access to the DOM (Document Object Model) as it interacts with web page elements.
- The conversation must be open and accessible in the DOM.
- The function is called with the appropriate permissions, considering browser security restrictions.

## Usage

1. Include the script containing the `enviarScript` function in your HTML document.
2. Ensure the conversation is open and accessible in the DOM.
3. Press F12, open console tab and paste raw script.
4. Enter to the `enviarScript` function with the desired script text.

## Parameters

- `scriptText`: A string containing the script to be sent as messages. Each line in the script will be treated as a separate message.

## Error Handling

The function may throw an error if no conversation is open. Ensure that a conversation is active in the DOM before calling the function.

## SHIPPING SPEED

`enviarScript(script, 2000)`

## Exemplo: --Novo Metodo funcional 2026 - [PT/BR]

```javascript
// Aguarda um elemento aparecer no DOM (necessário para React / WhatsApp Web)
function waitForElement(selector, root = document, timeout = 5000) {
    return new Promise((resolve, reject) => {
        const element = root.querySelector(selector);
        if (element) return resolve(element);

        const observer = new MutationObserver(() => {
            const el = root.querySelector(selector);
            if (el) {
                observer.disconnect();
                resolve(el);
            }
        });

        observer.observe(root, {
            childList: true,
            subtree: true
        });

        setTimeout(() => {
            observer.disconnect();
            reject(new Error(`Elemento não encontrado: ${selector}`));
        }, timeout);
    });
}

// Função principal de envio
async function enviarScript(scriptText, delay = 2000) {
    const lines = scriptText
        .split('\n')
        .map(l => l.trim())
        .filter(Boolean);

    const main = document.querySelector("#main");
    if (!main) throw new Error("Elemento #main não encontrado");

    const textarea = main.querySelector('div[contenteditable="true"]');
    if (!textarea) throw new Error("Não há conversa aberta");

    for (let i = 0; i < lines.length; i++) {
        const line = lines[i];
        console.log(`Enviando (${i + 1}/${lines.length}):`, line);

        // Insere o texto
        textarea.focus();
        document.execCommand('insertText', false, line);
        textarea.dispatchEvent(new Event('input', { bubbles: true }));

        // Espera o botão de enviar aparecer
        const sendButton = await waitForElement(
            '[data-testid="send"], [data-icon="send"], button[aria-label="Enviar"]',
            main,
            3000
        );

        await new Promise(r => setTimeout(r, 150));

        // Clica no botão (sem Enter)
        sendButton.click();

        if (i < lines.length - 1) {
            await new Promise(r => setTimeout(r, delay));
        }
    }

    return lines.length;
}

// ===============================
// ✏️ EDITE SEU TEXTO AQUI
// ===============================
const script = `
COLOQUE SEU TEXTO AQUI

Cada linha será enviada
como uma mensagem separada.

Você pode colar
qualquer texto aqui.
`;

// ▶️ EXECUÇÃO
enviarScript(script, 2000)
    .then(qtd => console.log(`Código finalizado: ${qtd} mensagens enviadas`))
    .catch(console.error);

```

## Example: --New functional method 2026 - [ENG/US]

```javascript
// Waits for an element to appear in the DOM (required for React / WhatsApp Web)
function waitForElement(selector, root = document, timeout = 5000) {
    return new Promise((resolve, reject) => {
        const element = root.querySelector(selector);
        if (element) return resolve(element);

        const observer = new MutationObserver(() => {
            const el = root.querySelector(selector);
            if (el) {
                observer.disconnect();
                resolve(el);
            }
        });

        observer.observe(root, {
            childList: true,
            subtree: true
        });

        setTimeout(() => {
            observer.disconnect();
            reject(new Error(`Element not found: ${selector}`));
        }, timeout);
    });
}

// Main sending function
async function enviarScript(scriptText, delay = 2000) {
    const lines = scriptText
        .split('\n')
        .map(l => l.trim())
        .filter(Boolean);

    const main = document.querySelector("#main");
    if (!main) throw new Error("Element #main not found");

    const textarea = main.querySelector('div[contenteditable="true"]');
    if (!textarea) throw new Error("No open conversation found");

    for (let i = 0; i < lines.length; i++) {
        const line = lines[i];
        console.log(`Sending (${i + 1}/${lines.length}):`, line);

        // Insert text into the input
        textarea.focus();
        document.execCommand('insertText', false, line);
        textarea.dispatchEvent(new Event('input', { bubbles: true }));

        // Wait for the send button to appear
        const sendButton = await waitForElement(
            '[data-testid="send"], [data-icon="send"], button[aria-label="Enviar"]',
            main,
            3000
        );

        await new Promise(r => setTimeout(r, 150));

        // Click the send button (no Enter key)
        sendButton.click();

        if (i < lines.length - 1) {
            await new Promise(r => setTimeout(r, delay));
        }
    }

    return lines.length;
}

// ===============================
// ✏️ EDIT YOUR TEXT HERE
// ===============================
const script = `
PUT YOUR TEXT HERE

Each line will be sent
as a separate message.

You can paste
any text here.
`;

// ▶️ EXECUTION
enviarScript(script, 2000)
    .then(qtd => console.log(`Finished: ${qtd} messages sent`))
    .catch(console.error);


In this example, the `enviarScript` function is called with a multi-line script, and the completion message or error is logged to the console.

Feel free to customize the script and adapt the function to fit your specific use case.

## 📝 License.

[![License](https://img.shields.io/github/license/vncsmnl/WhatsAppScripts?style=flat&logo=github&color=blue)](https://github.com/vncsmnl/WhatsAppScripts/blob/main/LICENSE)

```
            DO WHAT THE FUCK YOU WANT TO PUBLIC LICENSE
                    Version 2, December 2004

 Copyright (C) 2004 Sam Hocevar <sam@hocevar.net>

 Everyone is permitted to copy and distribute verbatim or modified
 copies of this license document, and changing it is allowed as long
 as the name is changed.

            DO WHAT THE FUCK YOU WANT TO PUBLIC LICENSE
   TERMS AND CONDITIONS FOR COPYING, DISTRIBUTION AND MODIFICATION

  0. You just DO WHAT THE FUCK YOU WANT TO.
```
