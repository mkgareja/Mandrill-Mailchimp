# Mandrill-Mailchimp

This tutorial will help you to setup mandrill-mailchimp intigration. follow the steps.

  1) [Create Mandrill accout] [mandrillac], Add domain, [Verify it][mandrillveri], [Create simple template][createtemp].
  
  2) [Create Mandrill accout] [mandrillac], [Connect with Mandrill.][connect-mandrill]
  
  3) [Send template form mailchimp to mandrill.][send-template] 
  
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



   
 

   [mandrillac]:<https://www.mandrill.com/signup/>
   [mandrillveri]:<https://www.youtube.com/watch?v=tP1ywBlPuf4>
   [createtemp]:<https://www.youtube.com/watch?v=BNFrStrhER8>
   [connect-mandrill]:<http://kb.mailchimp.com/integrations/other-integrations/mandrill-for-mailchimp-users>
   [send-template]:<https://mandrill.zendesk.com/hc/en-us/articles/205583097-How-do-I-add-a-MailChimp-template-to-my-Mandrill-account->
   [dns-mandrill]:<https://mandrill.zendesk.com/hc/en-us/articles/205582277-How-to-Add-DNS-Records-for-Sending-Domains>
   [inti]:<https://mandrillapp.com/api/docs/messages.php.html#method=send-template>

