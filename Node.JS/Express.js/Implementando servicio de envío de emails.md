# Servicio de Envío de Correos Electrónicos

Para implementar el servicio de envío de correos electrónicos en Node.js, se utiliza la librería Nodemailer. Esta librería permite enviar correos electrónicos de manera sencilla y flexible.

## Configuración del Servicio

El servicio de envío de correos electrónicos se implementa en un archivo separado, generalmente llamado `email.service.js`. Este servicio se encarga de enviar correos electrónicos con fines diversos, como notificaciones, confirmaciones de cuentas, recuperación de contraseñas, entre otros.

El servicio de envío de correos electrónicos generalmente contiene un método para enviar correos electrónicos a una dirección de correo electrónico específica. A continuación, se muestra un ejemplo de cómo podría ser este servicio:

```javascript
const nodemailer = require('nodemailer');
const { config } = require('../config/config');

class EmailService {
  async sendMail(email, subject, text, html) {
    try {
      const transporter = nodemailer.createTransport({
        host: 'smtp.gmail.com',
        secure: true,
        port: 465,
        auth: {
          user: config.mailerEmail,
          pass: config.mailerPassword,
        },
      });

      await transporter.sendMail({
        from: `"Foo Boo 👻" <${config.mailerEmail}>`,
        to: email,
        subject: subject,
        text: text,
        html: html,
      });

      return { message: 'Mail sent successfully' };
    } catch (error) {
      throw error;
    }
  }
}

module.exports = EmailService;
```

## Uso del Servicio en la Aplicación

Una vez que se ha implementado el servicio de envío de correos electrónicos, se puede utilizar en cualquier parte de la aplicación donde sea necesario enviar correos electrónicos. Por ejemplo, en un controlador de autenticación para enviar correos electrónicos de recuperación de contraseña:

```javascript
const express = require('express');
const AuthService = require('../../services/auth.service');

const router = express.Router();
const authService = new AuthService();

router.post('/recovery', async (req, res, next) => {
  try {
    const { email } = req.body;
    const subject = 'Password Recovery';
    const text = 'Please follow the instructions to reset your password.';
    const html = '<p>Please follow the instructions to reset your password.</p>';
    
    const response = await authService.sendMail(email, subject, text, html);
    res.json(response);
  } catch (error) {
    next(error);
  }
});

module.exports = router;
```

En este ejemplo, cuando se recibe una solicitud para recuperar la contraseña en el endpoint `/recovery`, se extrae el correo electrónico del cuerpo de la solicitud y se llama al método `sendMail` del servicio de autenticación para enviar un correo electrónico de recuperación de contraseña.
