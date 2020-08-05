# VoIP.ms-REST-for-PHP
 An example implementation of the VoIP.ms API using PHP

# Documentation
The Voip.ms API documentation can be found in the [Voip.ms Customer Portal](https://www.voip.ms/m/apidocs.php)

# Getting Started
You will have to enable API access from your account in the Customer Portal at Main Menu > SOAP and REST/JSON API or directly [here](https://www.voip.ms/m/api.php). 

In the same section, you can setup your API password and you'll have to add the IP address where the API is going to be used from. You can also use 0.0.0.0 as a wildcard, but this is discouraged for safety reasons.

![API Interface](https://i.imgur.com/aFEDkvg.png "API Interface")

Your API credentials need to be declared inside the code for the functions to work properly.

```PHP
$user = "john.doe@mydomain.com";
$pass = "johnspassword";

$ch = curl_init();
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true );
curl_setopt($ch, CURLOPT_URL, "https://voip.ms/api/v1/rest.php?api_username={$user}&api_password={$pass}&method={$method}");
$result = curl_exec($ch);
curl_close($ch);

$data=json_decode($result,true);

```
# Get Registration Status

```PHP
$method = "getRegistrationStatus";
$account = "100001_VoIP"; //Replace with the SIP/IAX Username of the Main or Sub Account in question


if($response[status]!='success'){
    echo $response[status];
    exit;
}

/* Is Registered */
echo "{$account} Registered : {$response[registered]}";

/* Get Registrations Array */
$registrations = $response[registrations];

/* Display Clients */
foreach($registrations as $registration){
    ?>
    <table style="border: 1px solid #336699; width:500px">
        <tr>
            <td>Server Name:</td>
            <td>
                <? echo $registration[server_name] ?>
            </td>
        <tr>
        
        <tr>
            <td>Server Short Name:</td>
            <td>
                <? echo $registration[server_shortname] ?>
            </td>
        <tr>
        
        <tr>
            <td>Server Hostame:</td>
            <td>
                <? echo $registration[server_hostname] ?>
            </td>
        <tr>
        
        <tr>
            <td>Server IP:</td>
            <td>
                <? echo $registration[server_ip] ?>
            </td>
        <tr>
        
        <tr>
            <td>Server Country:</td>
            <td>
                <? echo $registration[server_country] ?>
            </td>
        <tr>
        
        <tr>
            <td>Server POP:</td>
            <td>
                <? echo $registration[server_pop] ?>
            </td>
        <tr>
        
        <tr>
            <td>Register IP:</td>
            <td>
                <? echo $registration[register_ip] ?>
            </td>
        <tr>
        
        <tr>
            <td>Register Port:</td>
            <td>
                <? echo $registration[register_port] ?>
            </td>
        <tr>
        
        <tr>
            <td>Next Registration:</td>
            <td>
                <? echo $registration[register_next] ?>
            </td>
        <tr>
       
    </table>
    <br><br><br>
    <?
```

# Client Login
```PHP
$method = "getClients";
$email = "Jane.doe@mydomain.com";
$password = "janespassword";

$ch = curl_init();
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true );
curl_setopt($ch, CURLOPT_URL, "https://voip.ms/api/v1/rest.php?api_username={$user}&api_password={$pass}&method={$method}&email={$email}");
$result = curl_exec($ch);
curl_close($ch);

$response=json_decode($result,true);

/* Get Errors - Invalid_Client */
if($response[status]!='success'){
    echo $response[status];
    exit;
}

/* See if Password is Correct */
$client = $response[clients][0];
if($password!=$client[password]){
    echo "invalid_password";
    exit;
}

/* Client Exists and Password OK */
echo "{$client[client]} - {$client[firstname]} {$client[lastname]}"

?>
```

# Get Client Accounts Information
```PHP

$method = "getSubAccounts";
$client = "500000";

/* Get Errors - Invalid_Account */
if($response[status]!='success'){
    echo $response[status];
    exit;
}

/* Get Accounts Array */
$accounts = $response[accounts];

/* Display Accounts */
foreach($accounts as $account){
    ?>
    <table style="border: 1px solid #336699; width:500px">
        <tr>
            <td>Account:</td>
            <td>
                <? echo $account[account]; ?>
            </td>
        <tr>
        
        <tr>
            <td>Username:</td>
            <td>
                <? echo $account[username]; ?>
            </td>
        <tr>
        
        <tr>
            <td>Description:</td>
            <td>
                <? echo $account[description]; ?>
            </td>
        <tr>
        
        <tr>
            <td>Protocol:</td>
            <td>
                <? echo $account[protocol]; ?>
            </td>
        <tr>
        
        <tr>
            <td>Authorizacion Type:</td>
            <td>
                <? echo $account[auth_type]; ?>
            </td>
        <tr>
        
        <tr>
            <td>Password:</td>
            <td>
                <? echo $account[password]; ?>
            </td>
        <tr>
        
        <tr>
            <td>IP:</td>
            <td>
                <? echo $account[ip]; ?>
            </td>
        <tr>
        
        <tr>
            <td>Device Type:</td>
            <td>
                <? echo $account[device_type]; ?>
            </td>
        <tr>
        
        <tr>
            <td>CallerID Number:</td>
            <td>
                <? echo $account[callerid_number]; ?>
            </td>
        <tr>
        
        <tr>
            <td>Allow International Calls:</td>
            <td>
                <? echo $account[lock_international]; ?>
            </td>
        <tr>
        
        <tr>
            <td>International Route:</td>
            <td>
                <? echo $account[international_route]; ?>
            </td>
        <tr>
        
        <tr>
            <td>Music on Hold:</td>
            <td>
                <? echo $account[music_on_hold]; ?>
            </td>
        <tr>
        
        <tr>
            <td>Allowed Codecs:</td>
            <td>
                <? echo $account[allowed_codecs]; ?>
            </td>
        <tr>
        
        <tr>
            <td>DTMF Mode:</td>
            <td>
                <? echo $account[dtmf_mode]; ?>
            </td>
        <tr>
        
        <tr>
            <td>NAT:</td>
            <td>
                <? echo $account[nat]; ?>
            </td>
        <tr>
        
        <tr>
            <td>Internal Extension:</td>
            <td>
                <? echo $account[internal_extension]; ?>
            </td>
        <tr>
        
        <tr>
            <td>Internal Voicemail:</td>
            <td>
                <? echo $account[internal_voicemail]; ?>
            </td>
        <tr>
        
        <tr>
            <td>Internal Dialtime:</td>
            <td>
                <? echo $account[internal_dialtime]; ?>
            </td>
        <tr>
        
        <tr>
            <td>Reseller Client:</td>
            <td>
                <? echo $account[reseller_client]; ?>
            </td>
        <tr>
        
        <tr>
            <td>Reseller Package:</td>
            <td>
                <? echo $account[reseller_package]; ?>
            </td>
        <tr>
        
        <tr>
            <td>Reseller Next Billing Date:</td>
            <td>
                <? echo $account[reseller_nextbilling]; ?>
            </td>
        <tr>
        
    </table>
    <br><br><br>
    <?
```

# Voicemail Options
```PHP
$method = "getVoicemails";
$mailbox = "900000";

/* Get Errors - Invalid_Account */
if($response[status]!='success'){
    echo $response[status];
    exit;
}

/* Get Accounts Array */
$accounts = $response[accounts];

/* Get Errors - Invalid_Voicemail */
if($response[status]!='success'){
    echo $response[status];
    exit;
}

/* Get Voicemails Array */
$voicemails = $response[voicemails];

/* Display Voicemails */
foreach($voicemails as $voicemail){
    ?>
    <table style="border: 1px solid #336699; width:500px">
        <tr>
            <td>Mailbox:</td>
            <td>
                <? echo $voicemail[mailbox] ?>
            </td>
        <tr>
        
        <tr>
            <td>Name:</td>
            <td>
                <? echo $voicemail[name] ?>
            </td>
        <tr>
        
        
        <tr>
            <td>Password:</td>
            <td>
                <? echo $voicemail[password] ?>
            </td>
        <tr>
        
        <tr>
            <td>Skip Password:</td>
            <td>
                <? echo $voicemail[skip_password]?"Yes":"No" ?>
            </td>
        <tr>
        
        <tr>
            <td>e-mail:</td>
            <td>
                <? echo $voicemail[email] ?>
            </td>
        <tr>
        
        <tr>
            <td>Attach Message to e-mail:</td>
            <td>
                <? echo $voicemail[attach_message] ?>
            </td>
        <tr>
        
        <tr>
            <td>Delete Message after emailed:</td>
            <td>
                <? echo $voicemail[delete_message] ?>
            </td>
        <tr>
        
        <tr>
            <td>Say Time Envelope:</td>
            <td>
                <? echo $voicemail[say_time] ?>
            </td>
        <tr>
        
        
        <tr>
            <td>Time Zone:</td>
            <td>
                <? echo $voicemail[timezone] ?>
            </td>
        <tr>
        
        <tr>
            <td>Say Caller ID:</td>
            <td>
                <? echo $voicemail[say_callerid] ?>
            </td>
        <tr>
        
        <tr>
            <td>Play Instructions before beep:</td>
            <td>
                <? echo $voicemail[play_instructions] ?>
            </td>
        <tr>
        
        <tr>
            <td>Language:</td>
            <td>
                <? echo $voicemail[language] ?>
            </td>
        <tr>
       
    </table>
    <br><br><br>
    <?
```
# Get Packages Information
```
$method = "getPackages";

/* Get Errors - Invalid_Package */
if($response[status]!='success'){
    echo $response[status];
    exit;
}

/* Get Packages Array */
$packages = $response[packages];

/* Display Packages */
foreach($packages as $package){
    ?>
    <table style="border: 1px solid #336699; width:500px">
        <tr>
            <td>Package:</td>
            <td>
                <? echo $package[package] ?>
            </td>
        <tr>
        
        <tr>
            <td>Name:</td>
            <td>
                <? echo $package[name] ?>
            </td>
        <tr>
        
        <tr>
            <td>Mark Up Fixed:</td>
            <td>
                <? echo $package[markup_fixed] ?>
            </td>
        <tr>
        
        <tr>
            <td>Mark Up Percentage:</td>
            <td>
                <? echo $package[markup_percentage] ?>
            </td>
        <tr>
        
        <tr>
            <td>Pulse:</td>
            <td>
                <? echo $package[pulse] ?>
            </td>
        <tr>
        
        <tr>
            <td>International Route:</td>
            <td>
                <? echo $package[international_route] ?>
            </td>
        <tr>
        
        <tr>
            <td>Montly Fee:</td>
            <td>
                <? echo $package[monthly_fee] ?>
            </td>
        <tr>
        
        <tr>
            <td>Setup Fee:</td>
            <td>
                <? echo $package[setup_fee] ?>
            </td>
        <tr>
        
        <tr>
            <td>Free Minutes:</td>
            <td>
                <? echo $package[free_minutes] ?>
            </td>
        <tr>
       
    </table>
    <br><br><br>
    <?
```

# Get Call Detail Records

```
$method = "getCDR";

/* Get Errors - no_cdr */
if($response[status]!='success'){
    echo $response[status];
    exit;
}

/* Get CDR Array */
$cdr = $response[cdr];

/* Calls */
$calls = count($cdr);

/* Duration / Total */
foreach($cdr as $call){
    $duration += $call[seconds];
    $total += $call[total];
}
$duration = secToTime($duration);

?>
<table cellspacing="0" cellpadding="6" style="border: 1px solid #336699">
    <tr style="border: 1px solid #336699">
        <td style="border: 1px solid #336699">
            Date
        </td>
        <td style="border: 1px solid #336699">
            CallerID
        </td>
        <td style="border: 1px solid #336699">
            Destination
        </td>
        <td style="border: 1px solid #336699">
            Description
        </td>
        <td style="border: 1px solid #336699">
            Duration
        </td>
        <td style="border: 1px solid #336699">
            Rate
        </td>
        <td style="border: 1px solid #336699">
            Total
        </td>
    
    </tr>
    <?
    foreach($cdr as $call){
        ?>
        <tr>
            <td>
                <? echo $call[date]; ?>
            </td>
            <td>
                <? echo $call[callerid]; ?>
            </td>
            <td>
                <? echo $call[destination]; ?>
            </td>
            <td>
                <? echo $call[description]; ?>
            </td>
            <td align="right">
                <? echo $call[duration]; ?>
            </td>
            <td align="right">
                <? echo $call[rate]; ?>
            </td>
            <td align="right">
                <? echo $call[total]; ?>
            </td>
        </tr>
        <?
    }
    ?>
    <tr>
        <td colspan="7" align="right">
            <? echo "Calls: {$calls} | Duration: {$duration} | Total: \${$total}"; ?>
        </td>
    </tr>
</table>

<?

/* Function to Calculate Time */
function secToTime($secs){
    if(!$secs){return 0;}
    
    $vals = array('h' => floor($secs / 3600), 
                  'm' => floor($secs % 3600 / 60), 
                  's' => $secs % 60); 

    $ret = array(); 

    $added = false; 
    foreach ($vals as $k => $v) { 
        if ($v > 0 || $added) { 
            $ret[] = ((strlen($v) == 1) && $added) ? "0$v" : $v; 
            $added = true;
        } 
    } 

    return join(':', $ret); 
}
```

# Get Reseller Customer CDR

```
$method = "getResellerCDR";
$client = 500000;

/* Get Errors - no_cdr */
if($response[status]!='success'){
    echo $response[status];
    exit;
}

/* Get CDR Array */
$cdr = $response[cdr];

/* Calls */
$calls = count($cdr);

/* Duration / Total */
foreach($cdr as $call){
    $duration += $call[seconds];
    $total += $call[total];
}
$duration = secToTime($duration);

?>
<table cellspacing="0" cellpadding="6" style="border: 1px solid #336699">
    <tr style="border: 1px solid #336699">
        <td style="border: 1px solid #336699">
            Date
        </td>
        <td style="border: 1px solid #336699">
            CallerID
        </td>
        <td style="border: 1px solid #336699">
            Destination
        </td>
        <td style="border: 1px solid #336699">
            Description
        </td>
        <td style="border: 1px solid #336699">
            Duration
        </td>
        <td style="border: 1px solid #336699">
            Cost
        </td>
    
    </tr>
    <?
    foreach($cdr as $call){
        ?>
        <tr>
            <td>
                <? echo $call[date]; ?>
            </td>
            <td>
                <? echo $call[callerid]; ?>
            </td>
            <td>
                <? echo $call[destination]; ?>
            </td>
            <td>
                <? echo $call[description]; ?>
            </td>
            <td align="right">
                <? echo $call[duration]; ?>
            </td>
            <td align="right">
                <? echo $call[total]; ?>
            </td>
        </tr>
        <?
    }
    ?>
    <tr>
        <td colspan="7" align="right">
            <? echo "Calls: {$calls} | Duration: {$duration} | Total: \${$total}"; ?>
        </td>
    </tr>
</table>

<?

/* Function to Calculate Time */
function secToTime($secs){
    if(!$secs){return 0;}
    
    $vals = array('h' => floor($secs / 3600), 
                  'm' => floor($secs % 3600 / 60), 
                  's' => $secs % 60); 

    $ret = array(); 

    $added = false; 
    foreach ($vals as $k => $v) { 
        if ($v > 0 || $added) { 
            $ret[] = ((strlen($v) == 1) && $added) ? "0$v" : $v; 
            $added = true;
        } 
    } 

    return join(':', $ret); 
}
```

# Support

Please note that we do NOT provide support with your programming language. The only support provided by our staff is for bugs, documentation errors, documentation missing or other questions regarding the functionality of the API. Support regarding the API will be addressed via the ticketing system only at [support@voip.ms](support@voip.ms). Our programmers do not have access to the Live Chat. 
