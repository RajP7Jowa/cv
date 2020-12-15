#WHMCS Only demo for 11-12-2020


Setup Administration Account
============================
	email		:	test@reak.in
	UserName*	:	rtest
	Password*	:	admin@123

User Account
============
	email*	:	rusr@usr.com
	pass*	:	usr@123	


Licence
=========
	Dev-<---Not get on public---->


File Hosting Project
====================
	https://www39.zippyshare.com/v/bS7Yvhrr/file.html


Module Example
==============
	https://github.com/eclipsed-ninja/nforce-whmcs-module
	

F-end
=================
	https://xd.adobe.com/view/229b0528-0075-4d11-93ff-b70e4f248b35-77c8/

API
=======
	https://www.customerpanel.nl/public/api/v1/

	✔️	Traffic Graph
		Power Control
	✔️	Re-Installation Options
		rDNS options



># API Documentation

Network (traffic graph API)
==================
get `network` traffic grpah data on api

> `Post` get_datatraffic_usage

 		method:			get_datatraffic_usage			string
 		api_id:			<api>							string
 		serer_id:		<server_id>						integer
 		period:			current_month, last_month		string
 
 * Responce : success
	```
	{
	"StatusCode":"1",
	"StatusMessage":"Success.",
	"0": {
		"Server_Id":"123",
		"Graph_Img": "http://example.org/yourgraph_123.png&amp;secret=xyz",
		"Total_Usage":"1"
		}
	}
	```
 * Responce : failure
	```
	{
	"StatusCode": "0",
	"StatusMessage": "API ID is missing."
	}
	```


OS (Reinstall Option API)
======================

> `Post` reinstall_oslist

			method:			reinstall_oslist			string
			api_id:			<api>						string
			serer_id:		<server_id>					integer
			
 * Responce : success
	```
	{
		"0": {
			"Os_Id": "3",
			"Os": "CentOS 7.2 64-bit"
		},
		"1": {
			"Os_Id": "1",
			"Os": "Ubuntu 16.04 32-bit"
		},
		"2": {
			"Os_Id": "2",
			"Os": "Ubuntu 16.04 64-bit"
		},
		"StatusCode": "1",
		"StatusMessage": "Success."
	}
	```
* Responce : fail
	```
	{
	"StatusCode": "0",
	"StatusMessage": "any msg Remote reboot is not activated on this server."
	}
	```


> `Post` reinstall

			method:			reinstall			string
			api_id:			<api>				string
			serer_id:		<server_id>			integer
			main_ip			<main_ip>			string
			os_id:			<Os ID>				int	
			
 * Responce : success
	```
	{
	"0": {
		"Server_Id": "123",
		"IP": "127.0.0.1",
		"Password": "4z93wMqT"
	},
	"StatusCode": "1",
	"StatusMessage": "Success."
	}
	```
* Responce : fail
	```
	{
	"StatusCode": "0",
	"StatusMessage": "Server is already in reinstallation list."
	}
	```

> `Post` reinstall_status

			method:			reinstall_status		string
			api_id:			<api>					string
			serer_id:		<server_id>				integer
			main_ip			<main_ip>				string
			os_id:			<Os ID>					int	
			
 * Responce : success
	```
	{
	"StatusCode": "1",
	"StatusMessage": "Server is installing."
	}
	```
* Responce : fail
	```
	{
	"StatusCode": "1",
	"StatusMessage": "Server is installing."
	}
	```

# my function demo

```
function provisioningmodule_actionNetworkFunction($vars)
{
    try {
        $templateFile = 'templates/<templ_file_name>';
        $response_api = api_functionCall();
        $success =true;
        $data = array(
            'templatefile' => $templateFile,
            'breadcrumb' => array(
                'stepurl.php?action=this&var=that' => '<objectName>',
            ),
            'vars' => $response_api
        );
    } catch (Exception $e) {
        $success =false;
        // Record the error in WHMCS's module log.
        logModuleCall();
        $msg = $e->getMessage();
    }
    if ($success) {
        return array('dataplot' => $data);
    } else {
        return array(
            'message' => "<div class='alert alert-warning alert-dismissible'><p> " . $msg. " <button'type='button' class='close' data-dismiss='alert'>&times;</button></p></div>",
        );
    }
}

function httpPostCurl(){
    ....
    //sent all curl
    return array("status"=>"1","data"=>$data)
}

function api_functionCall(){
    $api_responce = httpPostCurl($api['api_url'], $api_post_array);
        if ($api_responce['status']) {
            
            .....
            return $modified_data_return 
        }       
}
```
