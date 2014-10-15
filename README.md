apache
======

Apache Related Scrips

The perl script uses the Parse::Apache::ServerStatus to fetch the apache statistics.

The scripts takes the hostname/ipaddress as the only argurement.if none is passed , "localhost" is used.

The script uses hostname to create the apache server-status url. http://hostname/server-status

Please make sure that server-status is enabled on server.

To enable the server status check the following configuration in the server httpd.conf,following 9 lines should be uncomment in configuration.

(1) LoadModule status_module modules/mod_status.so
(2) ExtendedStatus On
(3) < Location /server-status >
(4) SetHandler server-status
(5) Order deny,allow
(6) Deny from all
(7) Allow from 127.0.0.1
(8) Allow from < the script source ip address>
(9) </Location>
#################### OUTPUT #############################################################
p Parents (this key will be kicked in future releases, dont use it)

r Requests currenty being processed

i Idle workers

_ Waiting for Connection

S Starting up
R Reading Request
# W Sending Reply
# K Keepalive (read)
# D DNS Lookup
# C Closing connection
# L Logging
# G Gracefully finishing
# I Idle cleanup of worker
# . Open slot with no current process
###### The following keys are set to 0 if extended server-status is not activated. ########
# ta Total accesses
# tt Total traffic
# rs Requests per second
# bs Bytes per second
# br Bytes per request
################################ SAMPLE OUTPUT ##################################################################
# Command:
#
# perl parse_status.pl localhost
#
# Output:

#Fetching URL...http://localhost/server-status
#
# p r i _ S R W K D C L G I . ta tt rs bs br
# 0 1 8 8 0 0 1 0 0 0 0 0 0 247 451 520 kB .166 196 1180
# 0 1 8 8 0 0 1 0 0 0 0 0 0 247 452 524 kB .166 197 1187
# 0 1 8 8 0 0 1 0 0 0 0 0 0 247 458 531 kB .168 199 1187
# 0 1 8 8 0 0 1 0 0 0 0 0 0 247 460 536 kB .168 200 1193
# 0 1 8 8 0 0 1 0 0 0 0 0 0 247 461 540 kB .168 201 1199
# 0 1 8 8 0 0 1 0 0 0 0 0 0 247 463 545 kB .168 202 1205
# 0 1 8 8 0 0 1 0 0 0 0 0 0 247 464 549 kB .168 202 1211
# 0 1 8 8 0 0 1 0 0 0 0 0 0 247 465 554 kB .167 204 1219
#
################################################################################################################################################
