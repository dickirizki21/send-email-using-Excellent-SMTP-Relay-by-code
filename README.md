# Send email using Excellent SMTP Relay by code/programming.

Do you using zimbra and want send email by code?.

i will be sharing to you how to send email using **Excellent SMTP Relay Code**.

PHP Code for Send Email Using SMTP Relay.
------

1.  Native.

If you use php native, you can use [PHP Mailer](https://github.com/PHPMailer/PHPMailer). PHPMailer is available on Packagist (using semantic versioning), and installation via Composer is the recommended way to install PHPMailer. Just add this line to your ```composer.json``` file:
```php
"phpmailer/phpmailer": "^6.5"
```
or run
```php
composer require phpmailer/phpmailer
```
After ```PHPMailer``` already install u can try this PHP example:
```php
<?php
//Import PHPMailer classes into the global namespace
//These must be at the top of your script, not inside a function
use PHPMailer\PHPMailer\PHPMailer;
use PHPMailer\PHPMailer\SMTP;
use PHPMailer\PHPMailer\Exception;

//Load Composer's autoloader
require 'vendor/autoload.php';

//Create an instance; passing `true` enables exceptions
$mail = new PHPMailer(true);

try {
    //Server settings
    $mail->SMTPDebug = SMTP::DEBUG_SERVER;                      //Enable verbose debug output
    $mail->isSMTP();                                            //Send using SMTP
    $mail->Host       = 'relay.excellent.co.id';                     //Set the SMTP server to send through
    $mail->SMTPAuth   = true;                                   //Enable SMTP authentication
    $mail->Username   = 'relay.vavai@excellent.co.id';                     //SMTP username
    $mail->Password   = 'StdPwdStrong2021!';                               //SMTP password
    $mail->SMTPSecure = PHPMailer::ENCRYPTION_STARTTLS;            //Enable implicit TLS encryption
    $mail->Port       = 587;                                    //TCP port to connect to; use 587 if you have set `SMTPSecure = PHPMailer::ENCRYPTION_STARTTLS`

    //Recipients
    $mail->setFrom('from@example.com', 'Mailer');
    $mail->addAddress('user@example.net', 'Joe User');     //Add a recipient
    $mail->addAddress('user2@example.com');               //Name is optional
    $mail->addReplyTo('info@example.com', 'Information');
    $mail->addCC('cc@example.com');
    $mail->addBCC('bcc@example.com');

    //Attachments
    $mail->addAttachment('/var/tmp/file.tar.gz');         //Add attachments
    $mail->addAttachment('/tmp/image.jpg', 'new.jpg');    //Optional name

    //Content
    $mail->isHTML(true);                                  //Set email format to HTML
    $mail->Subject = 'Here is the subject';
    $mail->Body    = 'This is the HTML message body <b>in bold!</b>';
    $mail->AltBody = 'This is the body in plain text for non-HTML mail clients';

    $mail->send();
    echo 'Message has been sent';
} catch (Exception $e) {
    echo "Message could not be sent. Mailer Error: {$mail->ErrorInfo}";
}
```

2. CodeIgniter.

Download [CodeIgniter](https://codeigniter.com/download), here use CodeIgniter 3, and create file in ```aplication/controller```, this file for config send email with php and you can use library from Code Igniter and you can call the library ```$this->load->library('email', $config)```.

```php
<?php  
    if (!defined('BASEPATH'))exit('No direct script access allowed');

    class Export extends CI_Controller {

        public function __construct() {
            parent::__construct();
	    $this->load->model('site');
        }
		
        public function index(){
            $data['title'] = 'Create Excel | TechArise';
            $data['result'] = $this->site->getProduct();  
            $this->load->view('index', $data);
        }
		
		public function sendEmail() {
			
			$data['getInfo'] = $this->site->getProduct();
			$htmlContent = $this->load->view('generatepdffile', $data, TRUE);       
			
			$config = array(
				'protocol' => 'smtp', // 'mail', 'sendmail', or 'smtp'
				'smtp_host' => 'relay.excellent.co.id', 
				'smtp_user' => 'relay.vavai@excellent.co.id',
				'smtp_pass' => 'StdPwdStrong2021!',
				'smtp_port' => 587, // u can use 465 or 25 or 587
				'smtp_crypto' => 'tls', //can be 'ssl' or 'tls' for example
				'mailtype' => 'html', //plaintext 'text' mails or 'html'
				'charset' => 'utf-8',
				'newline' => "\r\n"
			);
		
			$this->load->library('email', $config);
			
			$from = 'from@domain.com';
			$to = 'to@domain.com';
			$subject = 'Example Subject';
			$message = 'hello this is test message';

			$this->email->set_newline("\r\n");
			$this->email->from($from);
			$this->email->to($to);
			$this->email->subject($subject);
			$this->email->message($htmlContent);

			if ($this->email->send()) {
				echo 'Your Email has successfully been sent.';
			} else {
				show_error($this->email->print_debugger());
			}
         }
        
    }
?>
```
Then you must be create view for ui send email, create file for view at ```aplication/views```.
```php
<div class="row">
    <div class="col-lg-12">
        <h2>Send Email using CodeIgniter Email Library</h2>                 
    </div>
</div><!-- /.row -->
<div class="row">
    <div class="col-lg-12">
       <a href="<?php echo base_url();?>export/sendEmail" class="pull-right btn btn-primary btn-xs" style="margin: 2px;"><i class="fa fa-plus"></i> Send Email</a>
    </div>
</div>
<hr>
<?php foreach($result as $detail){ ?>
		<table border="0" width="80%" align="center">
			<tr>
				<td width="5%"><?php echo $detail['id']; ?></td>
				<td width="12%"><img src="<?php echo base_url(); ?>assets/images/Penguins.jpg" height="85" width="75"></td>
				<td width="10%"><b>Price:</b> <?php echo number_format($detail['price'], 2, '.', ''); ?></td>
				<td width="30%"><b>Name:</b> <?php echo $detail['name']; ?></td>
				<td width="43%"><b>Descriptipn:</b> <?php echo $detail['description']; ?></td>
			</tr>
		</table>
		<hr>
<?php } ?>
```

and create file for fill bodytext email at ```aplication/views```.
```php
<style>
h1{
	font-size:25px;
	color:blue;
}
table{
	margin-top:20px;
}
</style>
<h1 align="center"> Products Report </h1><hr>
<br/><br/>
<?php foreach($getInfo as $detail){ ?>
		<table border="0">
			<tr>
				<td width="5%"><?php echo $detail['id']; ?></td>
				<td width="12%"><img src="<?php echo base_url(); ?>assets/images/Penguins.jpg" height="85" width="75"></td>
				<td width="10%"><b>Price:</b> <?php echo number_format($detail['price'], 2, '.', ''); ?></td>
				<td width="30%"><b>Name:</b> <?php echo $detail['name']; ?></td>
				<td width="43%"><b>Descriptipn:</b> <?php echo $detail['description']; ?></td>
			</tr>
		</table>
		<hr>
<?php } ?>
```

and the last u must create model file for connect both at ```aplication/models```.
```php
<?php
class Site extends CI_Model{
	
	public function getProduct($id = ''){
		$this->db->select('*');
		$this->db->from('products');
		if($id != ''){
			$this->db->where('id',$id);
		}
		return $this->db->get()->result_array();
	}
}
?>
```

now you can test sen email by browser.
 
3. Yii

* donwnload the extension from path [Yii Mail](http://code.google.com/p/yii-mail/downloads/list).
* Place the extracted folder inside the extensions folder.
* Modify the config file main.php like below,

```php
'mail' => array(
				'class' => 'ext.yii-mail.YiiMail',
				'transportType'=>'smtp',
				'transportOptions'=>array(
						'host'=>'relay.excellent.co.id',
						'username'=>'relay.vavai@excellent.co.id',
						'password'=>'StdPwdStrong2021!',
						'port'=>'587', // u can use 465 or 587 or 25						
				),
				'viewPath' => 'application.views.mail',	
		
		),
```
Hint: The view path points to '/protected/views/mail'.

* Import the extension in the main.php file.
```php
'ext.yii-mail.YiiMailMessage',
```
* Controller function to send the mail.

```php
public function SendMail()
	{	
		$message		= new YiiMailMessage;
           //this points to the file test.php inside the view path
		$message->view		= "test";
		$sid                 	= 1;
		$criteria            	= new CDbCriteria();
		$criteria->condition 	= "studentID=".$sid."";			
		$studModel1 	     	= Student::model()->findByPk($sid);		
		$params              	= array('myMail'=>$studModel1);
		$message->subject    	= 'My TestSubject';
		$message->setBody($params, 'text/html');				
		$message->addTo('yourmail@domain.com');
		$message->from = 'admin@domain .com';	
		Yii::app()->mail->send($message);		
	}

```

```php
 test.php file
```

```php
<html>
		<head>
		</head>
		<body>
			Dear <?php 
			 echo $myMail->studentName;
			 ?>
 				<br>This is a test mail.
		</body>
	   </html>
```

4. SWAKS

You can send email using excellent SMPT relay using [SWAKS](https://docs.oracle.com/en-us/iaas/Content/Email/Reference/swaks.htm)
, Swaks can be used to send test mails of all kinds. The advantage of Swaks compared to sending mails with your normal e-mail client is that you are able to alter almost any part of the e-mail: to, from, header, attachments, which server to speak to, etc.

Here are some common Swaks usage examples:
* Ensure Email Delivery is configured to send email. See Getting Started with Email Delivery.
* Ensure Swaks is installed. The installation process differs depending on which operating system you are using. For example, run the following command to install Swaks on Oracle Linux:

```sudo yum install swaks -y```
* To send a test email with Swaks, run the following command:

```swaks --pipeline -tls --server <smtp.region.oraclecloud.com> --port <587 or 25> --auth-user '<username OCID from SMTP credentials>' --auth-pass '<password>' --from '<sender email address>' --to '<recipient email address>' --data '<email message>'```
#### For example:
```swaks --pipeline -tls --server mail.hits.co.id --port 587 --auth-user 'hcis@hits.co.id' --auth-pass 'hits123456' --from 'sender@example.com' --to 'recipient@example.com' --data 'From: sender@example.com\nDate: Thu, 13 Sep 2019\nSubject: Test Send\n\nTest email'```


### Thank You for sharing , Good Luck
