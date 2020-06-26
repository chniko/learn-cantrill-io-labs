
To save time later in the DEMO we should populate this before configuring the ONPREM environment.
There are two VPN connections ... one between AWS and ONPREM ROUTER1 and one between AWS and ONPREM ROUTER2
For each of those there are two tunnels ... AWS Endpoint A -> ONPREMROUTER
and AWS endpointB -> ONPREMROUTER

Those are the details we will populate

# SHARED VALUES

ROUTER1_PRIVATE_IP                  = 192.168.12.194	
ROUTER2_PRIVATE_IP                  = 192.168.12.5
ONPREM BGP ASN                      = 65016
AWS BGP ASN                         = 64512

# CONNECTION1 - AWS => ON PREM ROUTER1

CONN1_TUNNEL1_PresharedKey          = xSrAYG0bY006Bzc5frsWePWvqq9D4zBn
CONN1_TUNNEL1_ONPREM_OUTSIDE_IP     = 18.215.184.9
CONN1_TUNNEL1_AWS_OUTSIDE_IP        = 13.248.213.68
CONN1_TUNNEL1_ONPREM_INSIDE_IP      = 169.254.241.246/30
CONN1_TUNNEL1_AWS_INSIDE_IP         = 169.254.241.245/30
CONN1_TUNNEL1_AWS_BGP_IP            = 169.254.241.245

CONN1_TUNNEL2_PresharedKey          = _z.1kXntyzOfvOuSX_6484Gy3nolApuK
CONN1_TUNNEL2_ONPREM_OUTSIDE_IP     = 18.215.184.9
CONN1_TUNNEL2_AWS_OUTSIDE_IP        = 99.83.177.229
CONN1_TUNNEL2_ONPREM_INSIDE_IP      = 169.254.149.202/30
CONN1_TUNNEL2_AWS_INSIDE_IP         = 169.254.149.201/30
CONN1_TUNNEL2_AWS_BGP_IP            = 169.254.149.201


# CONNECTION2 - AWS => ON PREM ROUTER2

CONN2_TUNNEL1_PresharedKey          = 
CONN2_TUNNEL1_ONPREM_OUTSIDE_IP     = 
CONN2_TUNNEL1_AWS_OUTSIDE_IP        = 
CONN2_TUNNEL1_ONPREM_INSIDE_IP      = 
CONN2_TUNNEL1_AWS_INSIDE_IP         = 
CONN2_TUNNEL1_AWS_BGP_IP            = 

CONN2_TUNNEL2_PresharedKey          = 
CONN2_TUNNEL2_ONPREM_OUTSIDE_IP     = 
CONN2_TUNNEL2_AWS_OUTSIDE_IP        = 
CONN2_TUNNEL2_ONPREM_INSIDE_IP      = 
CONN2_TUNNEL2_AWS_INSIDE_IP         = 
CONN2_TUNNEL2_AWS_BGP_IP            = 



# INSTRUCTIONS ON GETTING THE VALUES

We will be locating values for a specific connection `CONN1` or `CONN2` and a specific tunnel .. `TUNNEL1` or `TUNNEL2`

For anything starting with CONN1 .. Look in the `CONNECTION1CONFIG.TXT` file
For anything starting with CONN2 .. Look in the `CONNECTION2CONFIG.TXT` file
In each of the above files, for anything showing TUNNEL1 fine the section `IPSec Tunnel #1` in the above files
In each of the above files, for anything showing TUNNEL2 fine the section `IPSec Tunnel #2` in the above files

For `ROUTER1_PRIVATE_IP` its the 192.168.12.SOMETHING Private IPv4 Address for `ROUTER1` - get this from the EC2 Console
For `ROUTER2_PRIVATE_IP` its the 192.168.12.SOMETHING Private IPv4 Address for `ROUTER2` - get this from the EC2 Console
For `PreSharedKey` values above (one per tunnel (2) and per connection for a total of (4) look for `#1: Internet Key Exchange Configuration` in each tunnel section in each file, locate `- Pre-Shared Key  ` the value is there)
For `CONN1_TUNNEL1_ONPREM_OUTSIDE_IP` its the PublicIPv4 Address of `ROUTER1` 
    `CONN1_TUNNEL2_ONPREM_OUTSIDE_IP` its the PublicIPv4 Address of `ROUTER1` 
    `CONN2_TUNNEL1_ONPREM_OUTSIDE_IP` its the PublicIPv4 Address of `ROUTER2` 
    `CONN2_TUNNEL2_ONPREM_OUTSIDE_IP` its the PublicIPv4 Address of `ROUTER2` 

For `CONN1_TUNNEL1_AWS_OUTSIDE_IP` open `CONNECTION1CONFIG.TXT`, locate `IPSec Tunnel #1`, locate `#3: Tunnel Interface Configuration`, locate `Outside IP Addresses:`, locate `- Virtual Private Gateway` the value is there
For `CONN1_TUNNEL2_AWS_OUTSIDE_IP` open `CONNECTION1CONFIG.TXT`, locate `IPSec Tunnel #2`, locate `#3: Tunnel Interface Configuration`, locate `Outside IP Addresses:`, locate `- Virtual Private Gateway` the value is there
For `CONN2_TUNNEL1_AWS_OUTSIDE_IP` open `CONNECTION2CONFIG.TXT`, locate `IPSec Tunnel #1`, locate `#3: Tunnel Interface Configuration`, locate `Outside IP Addresses:`, locate `- Virtual Private Gateway` the value is there
For `CONN2_TUNNEL2_AWS_OUTSIDE_IP` open `CONNECTION2CONFIG.TXT`, locate `IPSec Tunnel #2`, locate `#3: Tunnel Interface Configuration`, locate `Outside IP Addresses:`, locate `- Virtual Private Gateway` the value is there

For `CONN1_TUNNEL1_ONPREM_INSIDE_IP` open `CONNECTION1CONFIG.TXT`, locate `IPSec Tunnel #1`, locate `#3: Tunnel Interface Configuration`, locate `Inside IP Addresses:`, locate `- Customer Gateway` the value is there
For `CONN1_TUNNEL2_ONPREM_INSIDE_IP` open `CONNECTION1CONFIG.TXT`, locate `IPSec Tunnel #2`, locate `#3: Tunnel Interface Configuration`, locate `Inside IP Addresses:`, locate `- Customer Gateway` the value is there
For `CONN2_TUNNEL1_ONPREM_INSIDE_IP` open `CONNECTION2CONFIG.TXT`, locate `IPSec Tunnel #1`, locate `#3: Tunnel Interface Configuration`, locate `Inside IP Addresses:`, locate `- Customer Gateway` the value is there
For `CONN2_TUNNEL2_ONPREM_INSIDE_IP` open `CONNECTION2CONFIG.TXT`, locate `IPSec Tunnel #2`, locate `#3: Tunnel Interface Configuration`, locate `Inside IP Addresses:`, locate `- Customer Gateway` the value is there

For `CONN1_TUNNEL1_AWS_INSIDE_IP` open `CONNECTION1CONFIG.TXT`, locate `IPSec Tunnel #1`, locate `#3: Tunnel Interface Configuration`, locate `Inside IP Addresses:`, locate `- Virtual Private Gateway` the value is there
For `CONN1_TUNNEL2_AWS_INSIDE_IP` open `CONNECTION1CONFIG.TXT`, locate `IPSec Tunnel #2`, locate `#3: Tunnel Interface Configuration`, locate `Inside IP Addresses:`, locate `- Virtual Private Gateway` the value is there
For `CONN2_TUNNEL1_AWS_INSIDE_IP` open `CONNECTION2CONFIG.TXT`, locate `IPSec Tunnel #1`, locate `#3: Tunnel Interface Configuration`, locate `Inside IP Addresses:`, locate `- Virtual Private Gateway` the value is there
For `CONN2_TUNNEL2_AWS_INSIDE_IP` open `CONNECTION2CONFIG.TXT`, locate `IPSec Tunnel #2`, locate `#3: Tunnel Interface Configuration`, locate `Inside IP Addresses:`, locate `- Virtual Private Gateway` the value is there

For `CONN1_TUNNEL1_AWS_BGP_IP` the value is the same as `CONN1_TUNNEL1_AWS_INSIDE_IP`
For `CONN1_TUNNEL2_AWS_BGP_IP` the value is the same as `CONN1_TUNNEL2_AWS_INSIDE_IP`
For `CONN2_TUNNEL1_AWS_BGP_IP` the value is the same as `CONN2_TUNNEL1_AWS_INSIDE_IP`
For `CONN2_TUNNEL2_AWS_BGP_IP` the value is the same as `CONN2_TUNNEL2_AWS_INSIDE_IP`

