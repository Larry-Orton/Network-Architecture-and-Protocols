
# Hi, I'm Larry! 👋

## This is a TCPDump and Wireshark project I wokred on.


# Applying Filters to TCPDump and Wireshark

This lab exercise is designed to allow the trainee to become familiar with applying a capture filter to TCPDump and Wireshark using Berkley Packet Filter (BPF) syntax.

## 1

open a terminal window (click Terminal icon in dock) and change current working directory by running the following command:

cd /home/student/Desktop/captures

## 2

here are a few packet capture files in this directory, and we will use TCPDump to read the capture file Lab 2.2.3-3.pcap to display the traffic. Using various options on the command line we will display only TCP packets, print the data in hexadecimal and ASCII output with link-level headers, and will not perform name resolutions on the addresses in the captured file. To do so, type the following into the command line:

tcpdump -n -XX tcp -r "Lab 2.2.3-3.pcap" | less



What ports and protocols do you see in this capture?

Since we are just displaying a packet capture file we do not need to use sudo. If you shift to using TCPDump to perform live capture then make sure you use sudo with it.

Additionally use quotes around file strings (like file names) that include spaces. If there are spaces in a file name Linux will interpret those spaces as the end of a string, vice seeing the space(s) as part of the file name.

The addition of the "| less" allows us to look at the traffic in smaller chunks. Hit the Spacebar key to advance through the pcap file and hit the q key to exit out of the more command.

## 3

In the last step we had a lot to look at. This time, we will be using filters to focus in on the items we are interested in. Right now, we are only interested in web (HTTP) traffic. To look at only that specific traffic you will need to add the necessary filtering option and syntax to your TCPDump command:

tcpdump -n -XX tcp port 80 -r "Lab 2.2.3-3.pcap" | less

Now that this filter is applied, do you see any other protocols such as ARP, DNS or FTP traffic? Make a list of the IP addresses of the web servers.

192.168.0.25.1112
172.16.20.20.80
192.168.0.25.1113
192.16.20.24.80
192.168.0.25.1114
172.16.20.24.80
Web servers will be responding on port 80.

## 4

Now we have a list of web servers, but we are only interested in one of them. Add the necessary syntax to your capture filter to capture only TCP port 80 and any host web server from your list for the host ip address.

tcpdump -n -XX host server_IP and tcp port 80 -r "Lab 2.2.3-3.pcap" | less

Using this new filter, do you see only the web server packets? Looking at the filtered traffic, do you see only inbound, only outbound or bi-directional (both directions of) traffic?

Remember to change the word SERVER_IP in command to the actual IP address you obtained in the previous step. If you enter the command as written exactly above you will receive an error.

##5

In Step 2 we had only one filter applied and saw all forms of TCP-related traffic in the capture file. While in Step 4, we had a couple of filters set which focused our attention to only port 80 TCP traffic related to a specific web server IP address. You should notice a significant difference in the packets displayed between Steps 2 and 4.

Look at the output you received at Step 2. Using that information, did that capture filter only display the packets of interest specified in Step 4?

## 6

Click on the Wireshark icon on the desktop sidebar. Open the same capture file, Lab 2.2.3-3.pcap.

## 7

Let's try to narrow down the results to what we are interested in. In the “Filter” field type (and hit the Apply button):

ip.dst_host contains "172.16" and http

What does this display filter do for us?

The filter we are using in Wireshark is known as a "display Filter."

Wireshark is also capable of using "capture filters" which, as the name implies, can be used while you use Wireshark to perform live traffic captures. The use of capture filters allows you to limit the type of traffic that is collected at that time - ignoring all the other traffic you might not be interested in. Capture filters should be applied with care as applying them will blind you to all but specifically what you set Wireshark to record.

## 8

You should now only have the packets we are interested in. Look up in the packet list window and click on the Source column name. What does this action do to our list of packets? Do the same action to the Destination and Protocol columns.

Note the IP addresses of the web servers. Does this current list of server IPs match the list you generated in Step 3?

## 9

Wireshark allows us to export entire HTML objects from a packet. Go to File -> Export Objects -> HTTP, select "packet num" 50, and then click Save As. Then, save it as http_object_one to the Desktop.

Then, close the object list, go the Desktop and view the exported object. Notice what was exported.

## 10

Go back to the Wireshark packet page, and then click click on the Clear button to remove the filter.

## 11

Change the capture filter to show only FTP sessions. Explore what occurred by using the Follow TCP Stream function to view the session details. Who logged in? What type of file did that user transfer? And what was the name of the file?

Before you close the stream, click Save As and save the RAW conversation to the Desktop as ftp_traffic.txt. Then close the stream and move to the next task.

## 12

Clear the FTP filter out and change it to look at only the Telnet-related traffic contained in the PCAP file. Review the activity captured by using the Follow TCP Stream function. What does it look like the user was doing?

Save this raw stream, too, as telnet_traffic.txt to the Desktop.

## 13

Clear out the filter field again. This time we want to see what non-TCP-related traffic was captured in this PCAP. To do this use a bang (!) symbol before tcp in the filter field. This is exactly opposite of what we did in Step 2. What protocols do you see now?


## Badges

[![Wireshark](https://img.shields.io/badge/Wireshark-Packet%20Capture-blue)](https://img.shields.io/badge/Wireshark-Packet%20Capture-blue)

[![Linux](https://img.shields.io/badge/Linux-Ubuntu-orange)](https://img.shields.io/badge/Wireshark-Packet%20Capture-blue)


