# Envío de Correo en Express

Utilizar un servicio de correo electrónico confiable es crucial para enviar enlaces de restablecimiento de contraseña o códigos de verificación. Aquí se presentan los conceptos generales para implementar un servicio de recuperación de contraseñas utilizando la librería Nodemailer.

## 1. **Instalación de Nodemailer**

Para comenzar, se necesita instalar la librería Nodemailer, que facilita el envío de correos electrónicos desde Node.js:

```bash
npm install nodemailer
```

## 2. **Configuración del Transporte de Correo**

Nodemailer requiere la configuración de un objeto de transporte que especifica cómo se enviarán los correos. Aquí se puede usar un servicio SMTP real o el servicio de prueba proporcionado por Ethereal.

### Ejemplo de Configuración con Ethereal

Ethereal es útil para pruebas ya que emula el envío de correos:

```javascript
const nodemailer = require('nodemailer');

async function main() {
  let testAccount = await nodemailer.createTestAccount();

  let transporter = nodemailer.createTransport({
    host: "smtp.ethereal.email",
    port: 587,
    secure: false,
    auth: {
      user: testAccount.user,
      pass: testAccount.pass,
    },
  });

  let info = await transporter.sendMail({
    from: '"Example Sender" <example@domain.com>',
    to: "recipient@domain.com",
    subject: "Password Recovery",
    text: "Click the link to reset your password.",
    html: "<b>Click the link to reset your password</b>",
  });

  console.log("Message sent: %s", info.messageId);
  console.log("Preview URL: %s", nodemailer.getTestMessageUrl(info));
}

main().catch(console.error);
```

### Ejemplo de Configuración con Gmail

Para un entorno de producción, se puede utilizar Gmail. Se debe crear una contraseña específica para la aplicación en la configuración de seguridad de la cuenta de Google:

```javascript
const nodemailer = require('nodemailer');

async function sendMail() {
  let transporter = nodemailer.createTransport({
    host: 'smtp.gmail.com',
    secure: true,
    port: 465,
    auth: {
      user: process.env.EMAIL_USER,
      pass: process.env.EMAIL_PASS,
    },
  });

  let info = await transporter.sendMail({
    from: '"Your App" <your_email@gmail.com>',
    to: 'user_email@example.com',
    subject: 'Password Recovery',
    text: 'Click the link to reset your password.',
    html: '<b>Click the link to reset your password</b>',
  });

  console.log('Message sent: %s', info.messageId);
}

sendMail().catch(console.error);
```

## 3. **Variables de Entorno**

Para mayor seguridad, las credenciales del correo electrónico (usuario y contraseña) deben almacenarse en variables de entorno:

```bash
EMAIL_USER=my_email@gmail.com
EMAIL_PASS=your_app_password
```

Estas se pueden cargar en la aplicación utilizando el paquete `dotenv`:

```javascript
require('dotenv').config();

const nodemailer = require('nodemailer');

async function sendMail() {
  let transporter = nodemailer.createTransport({
    host: 'smtp.gmail.com',
    secure: true,
    port: 465,
    auth: {
      user: process.env.EMAIL_USER,
      pass: process.env.EMAIL_PASS,
    },
  });

  let info = await transporter.sendMail({
    from: '"Your App" <your_email@gmail.com>',
    to: 'user_email@example.com',
    subject: 'Password Recovery',
    text: 'Click the link to reset your password.',
    html: '<b>Click the link to reset your password</b>',
  });

  console.log('Message sent: %s', info.messageId);
}

sendMail().catch(console.error);
```

## 4. **Enviar el Correo de Recuperación**

En el cuerpo del correo, se puede incluir un enlace para restablecer la contraseña que apunte a una ruta en la aplicación donde el usuario puede ingresar una nueva contraseña. Este enlace generalmente incluirá un token de seguridad para validar la solicitud.

```javascript
let resetLink = `https://yourapp.com/reset-password?token=${resetToken}`;
let info = await transporter.sendMail({
  from: '"Your App" <your_email@gmail.com>',
  to: user.email,
  subject: 'Password Recovery',
  text: `Click the link to reset your password: ${resetLink}`,
  html: `<b>Click the link to reset your password: <a href="${resetLink}">Reset Password</a></b>`,
});
```

## 5. **Implementación de Seguridad Adicional**

- **Tokens Seguros**: Generar tokens seguros y de un solo uso para los enlaces de restablecimiento de contraseñas.
- **Expiración de Tokens**: Establecer una expiración para los tokens de recuperación de contraseña.
- **Validación en el Servidor**: Validar los tokens en el servidor cuando el usuario haga clic en el enlace de recuperación para garantizar que sean válidos y no hayan expirado.