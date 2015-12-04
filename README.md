# Mandrill-Mailchimp
Best and easy way to Mandrill-Mailchimp integration. 

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

