# Config send mail by zimbra using PHP - Java

* Config for send mail For PHP.
```php
$config = array(
				'protocol' => '', //'mail', 'sendmail', or 'smtp'
				'smtp_host' => 'yourmail.co.id', 
				'smtp_user' => 'user.co.id',
				'smtp_pass' => 'passworduser',
                                'smtp_port' => 587, //587 or 465 or 25
				'smtp_crypto' => '', //can be 'ssl' or 'tls' for example
				'mailtype' => '', //plaintext 'text' mails or 'html'
				'charset' => 'utf-8',
				'newline' => "\r\n"
			);
```
* Config for send mail For Java.
```java
package com.example.smtp;package com.example.smtp;import java.util.Properties;
import javax.mail.Message;import javax.mail.MessagingException;
import javax.mail.PasswordAuthentication;import javax.mail.Session;
import javax.mail.Transport;import javax.mail.internet.InternetAddress;
import javax.mail.internet.MimeMessage;
public class SendHTMLEmail {   
public static void main(String[ ] args) {      
String to = "johndoe@gmail.com";
      String from = "yourmail@example.com";      
final String username = "yourlogin";      
final String password = "yourpassword";
      String host = "smtp.example.com";
      Properties props = new Properties();      
props.put("mail.smtp.auth", "true");      
props.put("mail.smtp.starttls.enable", "true");      
props.put("mail.smtp.host", host);      
props.put("mail.smtp.port", "2525");
      // Get the Session object      
Session session = Session.getInstance(props,         
new javax.mail.Authenticator() {            
protected PasswordAuthentication getPasswordAuthentication() {               
return new PasswordAuthentication(username, password);            
} 
});
      try {            
// Create a default MimeMessage object            
Message message = new MimeMessage(session);
    message.setFrom(new InternetAddress(from));
 message.setRecipients(Message.RecipientType.TO,              
InternetAddress.parse(to));
 message.setSubject("HTML message with an image and attachment");
    // Put your HTML content here as well as refer to the hosted image    
message.setContent(              
"<p><img src="https://yourserver.com/yourlogo.png" alt="img" /></p> +     
<p>Hey, do you like our logo?</p>",             
"text/html");
    // Send message    
Transport.send(message);
    System.out.println("Sent message successfully....");
      } catch (MessagingException e) {    
e.printStackTrace();    throw new RuntimeException(e);      
}   
}
}
```

      
### Documentation Send Email By Framework
* if you are using Code Igniter you can click link here [Doc SendEmail With Code Igniter](https://codeigniter.com/userguide3/libraries/email.html?__cf_chl_managed_tk__=4fd9af07df80f68bdb6ac675e61834ec44663146-1624856363-0-ARyxh8zm4SbESRW1FTHvoRANRL-RDWcHnJMW6CHqi_gEG6PfbJqnlDMfI7WzHnwUMA-A9AZFvOI25zlyI3ALdDgo_wbOkfPUKdhMhZFov2f7Lv71HlIdA74H0-Vx5RMwSOFkKS_vuc95-_aTWMdW7AI9rFjPNXFhhmoJ2GiPIEy3Ne2sKK01dR98NRWd50spDvyZOLgViQ8qM4ljZRrfmTUmtLvLr3nEt4MaZchOzJv1RWxoGyGdeICVS9_k8fJ2qs6-0VDs1p28TU199V0v83IMMa9CDQN1oLIwJ6UMW68Cw5KN6236r32PYCpTbDXg6Iy2TCN99gmCh1FPwVaP9b0jMj0fAXj38kXwmXPmv-GPrf3-8OCUvVgaE0Quyc5qO8qWvwDBP-L3qqu72h4a0Hm_tPhxBAMYM8KOwbqukaviyiaLJaKEwFf0sg4c8t3k9LF-gUPLlib5eQokO2si8gL94plbYfLTl1xfJJhi6r3zlFyeTGPbXDsJdJLweL4rROM9dOVkD31fEXXdLm8pt87qOwSiKI3oo6QQD9LKbteQVigdDXHHWgNhMn1MHuFnZSV1QjBFX0f9gKf1PJvfMj3WvWuxirtBzClpdjRksQHj2cwNbKzl3UQRLn9AVT2MQ8MTwFX2W-3yAURnt3PV64U)
* if you are using Yii framework you can click link here [Doc SendEmail With Yii](https://www.yiiframework.com/wiki/468/send-mail-using-yiimail-extension)

##### and this example send email using code igniter [send email using code igniter](https://github.com/vajirali/sendEmailbyCi.git) and this for [Doc SendEmail With Yii](https://jaxenter.com/java-app-emails-smtp-server-164144.html?__cf_chl_captcha_tk__=ea03a51d36ec7e0d2cc6ceeb92609fad1dc1c5e4-1624861873-0-ATqNd1670IIT5GlkooXsS7RfEjThirAi_uniLVkGdGHOs9jrDS0pxRSouk9ByP8IOaquCCmDuBr-8jyG6d9mSStH5fQNdhHPEK0_OHeb6fZmjg8KU2R4T4sbY7qJJlWWVXxI9Ejr1TlGemOfXV25JnS51AfYWWaURCSHOYkKZEScALuyuSwg9s_6WzqHtDiqUdWMJ6QksuUy_O9aeQ3Ijfd_6BaZqImOcljjL1u-LVTRIXwmlAyCEhC1Act3dQ9SyKWP8mhIFxgvaYU8hkySxXG9IjqCC7aAqUmv50aU2s6BdrqQPHT_WdweCyw1YlTGWUtM4j8YCHM8XvImMod-9xM9VDRv9vgINz8qjitxweW29BQ1JXaPOt3DT0pWmUbJrmwfVRSP_qhyHMWawfcYHjDHa24BDZT_dBjIyp8EaCkPhhXn_WDMuucRrYrlHKye72MCyeq29uxTDzzPNHER3zV9FXCKisGHjtvBRLLx2ns3oXJ3Gd0pc1wjtfowpPifw_xtti5LMcwnYndkS-KtIsjy_woVNN3AglY5ZLkEJDW_Kri-68Ha8J2zjt0sJPVW4daH5P0Xr-K88iM2BNbY7KGbeoRZvJ9TqFr-pPWWUu0HrQfKN6AN9wlGGH5E6pWugOdkmDVqWHWql4qV7SQ0v6Uf8xYxL6IQWoMkLEkHghCn) 

### Thank You, Goodl Luck
