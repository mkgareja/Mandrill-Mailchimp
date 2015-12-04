# Mandrill-Mailchimp

If you already have a MailChimp account, linking it to your Mandrill account allows you to take advantage of bundled pricing. For each MailChimp account, you can link to one Mandrill account. A Mandrill account can be linked to multiple MailChimp accounts.This tutorial will help you to setup mandrill-mailchimp intigration.

you can send emails through the Mandrill API or SMTP integration. With the Mandrill API, you can send emails, get information about your account, and view or parse reporting data in your own app or system. Point your developer to these resources to get started



  1) [Create Mandrill accout] [mandrillac]
  
  2)  Add a New Sending Domain
  
      -Go to Settings
      -Choose Sending Domains.
      -Type a new domain at the top and click Add.
      
  3) [Add DNS Records and Test Sending Domain Settings][mandrillveri]

  Now that you've added a new sending domain, [add the appropriate records][dns-link] to your domain's DNS settings.
  
  4) [Create Mailchimp accout] [mailchimpac]
  
    -In your MailChimp account, click your profile name to expand the Account Panel, and click Account.
    -Click the Integrations option.
    -Click the Mandrill option.
    -Click Authorize Connection.
    -You'll be redirected to the Mandrill login page to enter your Mandrill username and password.
    -After providing your Mandrill username and password, you'll see a message asking if you'd like to grant MailChimp access to your Mandrill account.
    -Grant MailChimp access to your Mandrill account
    -Click Allow to connect your accounts or Deny to cancel the connection attempt.
  
  [Connect with Mandrill.][connect-mandrill]
  
  5) [Send template form mailchimp to mandrill][send-template]
  
    -Navigate to the Templates page in your MailChimp account.
    -Locate the template you'd like to copy by browsing the template list or using the search option.
    -Click the template's drop-down menu and choose Send To Mandrill.
    -You'll see a success message once your template has been saved to your Mandrill account.
  But  templates in Mandrill work differently than in MailChimp, so you may need to tweak your templates for Mandrill.
  
  6) Now signin in mandrill
  
    -Navigate to the outboud in your Mandrill account.
    -Select templete page.
    -Here you can find listing of mailchimp template.
### API calls
[Official API Clients][inti]
### json:
```sh
{
    "key": "your_api_key",
    "template_name": "example template_name",
    "template_content": [
        {
            "name": "example name",
            "content": "example content"
        }
    ],
    "message": {
        "html": "<p>Example HTML content</p>",
        "text": "Example text content",
        "subject": "example subject",
        "from_email": "message.from_email@example.com",
        "from_name": "Example Name",
        "to": [
            {
                "email": "recipient.email@example.com",
                "name": "Recipient Name",
                "type": "to"
            }
        ],
        "headers": {
            "Reply-To": "message.reply@example.com"
        },
        "important": false,
        "track_opens": null,
        "track_clicks": null,
        "auto_text": null,
        "auto_html": null,
        "inline_css": null,
        "url_strip_qs": null,
        "preserve_recipients": null,
        "view_content_link": null,
        "bcc_address": "message.bcc_address@example.com",
        "tracking_domain": null,
        "signing_domain": null,
        "return_path_domain": null,
        "merge": true,
        "merge_language": "mailchimp"
    },
    "async": false,
    "ip_pool": "Main Pool"
}
```
### PHP:
```sh
<?php
try {
    $mandrill = new Mandrill('YOUR_API_KEY');
    $template_name = 'example template_name';
    $template_content = array(
        array(
            'name' => 'example name',
            'content' => 'example content'
        )
    );
    $message = array(
        'html' => '<p>Example HTML content</p>',
        'text' => 'Example text content',
        'subject' => 'example subject',
        'from_email' => 'message.from_email@example.com',
        'from_name' => 'Example Name',
        'to' => array(
            array(
                'email' => 'recipient.email@example.com',
                'name' => 'Recipient Name',
                'type' => 'to'
            )
        ),
        'headers' => array('Reply-To' => 'message.reply@example.com'),
        'important' => false,
        'track_opens' => null,
        'track_clicks' => null,
        'auto_text' => null,
        'auto_html' => null,
        'inline_css' => null,
        'url_strip_qs' => null,
        'preserve_recipients' => null,
        'view_content_link' => null,
        'bcc_address' => 'message.bcc_address@example.com',
        'tracking_domain' => null,
        'signing_domain' => null,
        'return_path_domain' => null,
        'merge' => true,
        'merge_language' => 'mailchimp'
    );
    $async = false;
    $ip_pool = 'Main Pool';
    $send_at = 'example send_at';
    $result = $mandrill->messages->sendTemplate($template_name, $template_content, $message, $async, $ip_pool);
    print_r($result);
} catch(Mandrill_Error $e) {
    // Mandrill errors are thrown as exceptions
    echo 'A mandrill error occurred: ' . get_class($e) . ' - ' . $e->getMessage();
    // A mandrill error occurred: Mandrill_Unknown_Subaccount - No subaccount exists with the id 'customer-123'
    throw $e;
}
?>
```

### nodejs:
```sh
mandrill_client = new mandrill.Mandrill('YOUR_API_KEY');
var message = {
    "html": "<p>Example HTML content</p>",
    "text": "Example text content",
    "subject": "example subject",
    "from_email": "message.from_email@example.com",
    "from_name": "Example Name",
    "to": [{
            "email": "recipient.email@example.com",
            "name": "Recipient Name",
            "type": "to"
        }],
    "headers": {
        "Reply-To": "message.reply@example.com"
    },
    "important": false,
    "track_opens": null,
    "track_clicks": null,
    "auto_text": null,
    "auto_html": null,
    "inline_css": null,
    "url_strip_qs": null,
    "preserve_recipients": null,
    "view_content_link": null,
    "bcc_address": "message.bcc_address@example.com",
    "tracking_domain": null,
    "signing_domain": null,
    "return_path_domain": null,
    "merge": true,
    "merge_language": "mailchimp"
};
var async = false;
var ip_pool = "Main Pool";
mandrill_client.messages.send({"message": message, "async": async, "ip_pool": ip_pool}, function(result) {
    console.log(result);
    /*
    [{
            "email": "recipient.email@example.com",
            "status": "sent",
            "reject_reason": "hard-bounce",
            "_id": "abc123abc123abc123abc123abc123"
        }]
    */
}, function(e) {
    // Mandrill returns the error as an object with name and message keys
    console.log('A mandrill error occurred: ' + e.name + ' - ' + e.message);
    // A mandrill error occurred: Unknown_Subaccount - No subaccount exists with the id 'customer-123'
});
```
### ruby:
```sh
begin
    mandrill = Mandrill::API.new 'YOUR_API_KEY'
    template_name = "example template_name"
    template_content = [{"content"=>"example content", "name"=>"example name"}]
    message = {"google_analytics_campaign"=>"message.from_email@example.com",
     "merge_language"=>"mailchimp",
     "inline_css"=>nil,
     "subaccount"=>"customer-123",
     "merge"=>true,
     "return_path_domain"=>nil,
     "url_strip_qs"=>nil,
     "track_clicks"=>nil,
     "headers"=>{"Reply-To"=>"message.reply@example.com"},
     "view_content_link"=>nil,
     "to"=>
        [{"type"=>"to",
            "email"=>"recipient.email@example.com",
            "name"=>"Recipient Name"}],
     "html"=>"<p>Example HTML content</p>",
     "google_analytics_domains"=>["example.com"],
     "from_name"=>"Example Name",
     "text"=>"Example text content"
     "tracking_domain"=>nil,
     "subject"=>"example subject",
     "signing_domain"=>nil,
     "auto_html"=>nil,
     "track_opens"=>nil,
     "from_email"=>"message.from_email@example.com",
     "auto_text"=>nil,
     "important"=>false}
    async = false
    ip_pool = "Main Pool"
    result = mandrill.messages.send_template template_name, template_content, message, async, ip_pool
        # [{"status"=>"sent",
        #     "reject_reason"=>"hard-bounce",
        #     "email"=>"recipient.email@example.com",
        #     "_id"=>"abc123abc123abc123abc123abc123"}]
    
rescue Mandrill::Error => e
    # Mandrill errors are thrown as exceptions
    puts "A mandrill error occurred: #{e.class} - #{e.message}"
    # A mandrill error occurred: Mandrill::UnknownSubaccountError - No subaccount exists with the id 'customer-123'
    raise
end
```

### Tips

 - Setup [DNS verification][dns-mandrill] of mandrill.
 - Generate api key from mandrill account.
 - Remove unwanted parameters from api call. 
 

 
## Reference
  - [Mandrill Docs][mndoc]
  - [Mailchimp Docs][mcdoc]
  - [Easy Techi][ET]

   
 

   [mandrillac]:<https://www.mandrill.com/signup/>
   [mailchimpac]:<https://login.mailchimp.com/signup>
   [mandrillveri]:<https://www.youtube.com/watch?v=tP1ywBlPuf4>
   [createtemp]:<https://www.youtube.com/watch?v=BNFrStrhER8>
   [connect-mandrill]:<http://kb.mailchimp.com/integrations/other-integrations/mandrill-for-mailchimp-users>
   [send-template]:<https://mandrill.zendesk.com/hc/en-us/articles/205583097-How-do-I-add-a-MailChimp-template-to-my-Mandrill-account->
   [dns-mandrill]:<https://mandrill.zendesk.com/hc/en-us/articles/205582277-How-to-Add-DNS-Records-for-Sending-Domains>
   [inti]:<https://mandrillapp.com/docs/integrations.html>
   [mndoc]:<https://mandrillapp.com/docs/>
   [mcdoc]:<http://developer.mailchimp.com/documentation/mailchimp/?_ga=1.173251683.1335557208.1449041276>
   [ET]:<https://www.youtube.com/watch?v=BNFrStrhER8>
   [create-temp]:<https://mandrill.zendesk.com/hc/en-us/articles/205583097-How-do-I-add-a-MailChimp-template-to-my-Mandrill-account->
   [dns-link]:<http://help.mandrill.com/entries/22030056-how-do-i-add-dns-records-for-my-sending-domains>

