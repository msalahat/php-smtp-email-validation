# PHP SMTP Email Validation #

**A PHP class that allows validation of email addresses via SMTP.**

Email Syntax can check whether an email address has a valid format, however, in order to check if the email address actually exists, you will have to query the email domain for the existence of the email address.

The PHP class encapsulates the SMTP transation between the remote domain, as well as the DNS lookup for the Mail Transfer Agent (MTA) responsible for that domain.

The class can take a number of email addresses, and return whether they are valid or not. It will group together emails with the same domain, and create a single SMTP connection to the MTA for those emails for efficiency.

This class is meant to be a secondary validation of an email address after the [email syntax](http://code.google.com/p/php-email-address-validation/) is validated. It can also provide intermediate email validation before sending a confirmation email to the email address, which does not provide user feedback if the email is invalid - and thus loss of users.

## Example Usage ##

Validating a Single Email address:
```
// include SMTP Email Validation Class
require_once('smtp_validateEmail.class.php');

// the email to validate
$email = 'user@example.com';
// an optional sender
$sender = 'user@mydomain.com';
// instantiate the class
$SMTP_Validator = new SMTP_validateEmail();
// turn on debugging if you want to view the SMTP transaction
$SMTP_Validator->debug = true;
// do the validation
$results = $SMTP_Validator->validate(array($email), $sender);
// view results
echo $email.' is '.($results[$email] ? 'valid' : 'invalid')."\n";

// send email? 
if ($results[$email]) {
  //mail($email, 'Confirm Email', 'Please reply to this email to confirm', 'From:'.$sender."\r\n"); // send email
} else {
  echo 'The email addresses you entered is not valid';
}
```

Validating Multiple Email addresses:
```
// include SMTP Email Validation Class
require_once('smtp_validateEmail.class.php');

// the email to validate
$emails = array('user@example.com', 'user2@example.com');
// an optional sender
$sender = 'user@yourdomain.com';
// instantiate the class
$SMTP_Validator = new SMTP_validateEmail();
// turn on debugging if you want to view the SMTP transaction
$SMTP_Validator->debug = true;
// do the validation
$results = $SMTP_Validator->validate($emails, $sender);

// view results
foreach($results as $email=>$result) {
        // send email? 
  if ($result) {
    //mail($email, 'Confirm Email', 'Please reply to this email to confirm', 'From:'.$sender."\r\n"); // send email
  } else {
    echo 'The email address '. $email.' is not valid';
  }
}

```

## Download ##

You can [browse the source code](http://code.google.com/p/php-smtp-email-validation/source/browse/#svn/trunk) for the latest version.

You may also download the [whole archive](http://code.google.com/p/php-smtp-email-validation/downloads/list) found in the download section. However, it may not be the latest version.