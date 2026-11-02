# Connected to Wi-Fi but No Internet

*Commands tested in Ubuntu and Windows 11 virtual machines.*

## Symptom

The customer says, "My Wi-Fi is connected, but no websites open."

## Cause

It depends on which test fails first. Possible causes are a DHCP failure (no IP address), a local connection problem, no internet from the router, or a DNS problem.

## Steps (run the tests in this order)

**1. Check for an IP address**
- Ubuntu: run `ip a`. Windows: run `ipconfig`.
- If there is no address, or it starts with `169.254`, DHCP has failed. Reconnect to Wi-Fi or restart the router.

**2. Ping the gateway**
- Ubuntu: run `ip route` and find the address after `default via`. Windows: find "Default Gateway" in `ipconfig`.
- Ping that address. If it fails, the problem is local: weak Wi-Fi signal, wrong password, or a blocked device.

**3. Ping 8.8.8.8**
- If it fails, the router is not getting internet. Restart the router, and if it still fails, contact the internet provider.

**4. Ping google.com**
- If this fails but step 3 worked, it is a DNS problem. Run `nslookup google.com` to confirm, then change the DNS server to 8.8.8.8 or restart the router.

**5. Test again** by opening a website.

## Expected result

A website opens.

## If it still doesn't work

Escalate the ticket with the result of each test.

## What I tested in my lab

- Turned off the virtual network cable in Ubuntu. `ip a` showed `NO-CARRIER`, the interface was `DOWN`, and `ping 8.8.8.8` said "Network is unreachable". Reconnecting fixed it.
- Asked a wrong DNS server with `nslookup google.com 1.2.3.4`. It timed out, while `ping 8.8.8.8` still worked.
- Ran `ipconfig`, `ping`, and `nslookup` on Windows 11 and saw the same values as on Ubuntu.

## Not tested

The router restart and provider steps are standard advice. I could not test them in a virtual machine.
