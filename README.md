## Quickstart with Nodemailer
In this page you're going to learn how to create a Node.js function to send an email using Nodemailer.
Start by opening your terminal and use the following command to install Nodemailer:
```
$ npm install nodemailer
```
Require Nodemailer at the top of your file:
``` javascript
const nodemailer = require("nodemailer");
```
Now you're going to create a main function to send our Nodemailer emails. Our function needs an email account to send from, if you don't already have an email address to use with Nodemailer, you can create an SMTP service test account from ethereal.mail. 
``` javascript
let testAccount = await nodemailer.createTestAccount()
```
Nodemailer's main transport for sending emails is an SMTP transporter because almost every email delivery provider supports SMTP. SMTP is also the protocol used to send emails between different hosts, so it is universally available.If you already have an email account simply substitute your email account information in the SMTP transporter:
``` javascript
let transporter = nodemailer.createTransport({
    host: "smtp.ethereal.email",
    port: 587,//uses port 465 if secure is true.
    secure: false,
    auth: { user: testAccount.user, pass: testAccount.password },
  });
```
Now you can use the transporter to send your email. Add your recipients, choose your subject line, and add your email in both html and plain text for best results.
``` javascript 
  let email = await transporter.sendMail({
    from: '"Example User" <testAccount.user>', // sender address
    to: "them@example.com, recipient@example.com", // list of recipients
    subject: "Hello World!", // Subject line
    text: "My first Nodemailer email!", // plain text body
    html: "<b>My first Nodemailer email!</b>", // html body
  });
```
Your main function should now look like this:
``` javascript
const main = () => {
let testAccount = await nodemailer.createTestAccount()

let transporter = nodemailer.createTransport({
    host: "smtp.ethereal.email",
    port: 587,//uses port 465 if secure is true.
    secure: false,
    auth: { user: testAccount.user, pass: testAccount.password },
  });
let email = await transporter.sendMail({
    from: '"Example User" <you@example.com>', // sender address
    to: "them@example.com, recipient@example.com", // list of recipients
    subject: "Hello World!", // Subject line
    text: "My first Nodemailer email!", // plain text body
    html: "<b>My first Nodemailer email!</b>", // html body
  });
  console.log("Email: "+email.messageId+" was sent.") //This prints to the console that the email has been sent.
}
```
And that's it! You now have a function to send emails using Nodemailer.
