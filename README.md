# high-traffic-site-optimization

Tools, techniques, principles, patterns and designs to have a high-performance Linux server.

## Two main approaches to apply optimization
Here are two ways to try to optimize a website; we have **top-down** and **bottom-up**.
in top-down approach people debate about which programming language is faster. They say
**WordPress** is slow and **ReactJS** is faster; which is true.  
**Python** is faster and **NodeJS**, yes true.  
So the point is, for having a really fast website, just *a faster programming language* cannot
help so much. For any website to function (be loaded) we have there four levels (layers):  
1. code level (php, go, python, etc)
2. service level (Apache, Nginx, LiteSpeed, etc)
3. architecture level (HA, LB, etc)
4. infrastructure level (network, dedicated server, VM, containers, etc)

We tested and realized that the same code, but in different **DataCenter** has different speed.
Just changing the DataCenter. So when we can apply optimization from *top to bottom* (which works)
we can apply it from *bottom-to-up* which is more effective.  

We are going to cover there four layers and provide solutions for each laster and improve overall
performance of the website we have.

**NOTE**  
SVGs are used to better demonstration.



### Top-Down (ineffective)

<p align="center">
    <img src="svg/ineffective-top-down.svg" />
</p>

### Bottom-Up (effective)

<p align="center">
    <img src="svg/effective-bottom-up.svg" />
</p>

<hr>

### Infrastructure
Check / test your infrastructure  

#### dmidecode
dmidecode - DMI table decoder  
dmidecode  is a tool for dumping a computer's DMI (some say SMBIOS) table contents in a human-readable format. 

Usage
`dmidecode --type | -t`  
options
```
bios
system
baseboard
chassis
processor
#memory
cache
connector
slot
```
There of the are more useful  
```
sudo dmidecode --type system
sudo dmidecode --type processor
sudo dmidecode --type memory
```


Test on a dedicated #server (`sudo dmidecode --type system`)
```
System Information
Manufacturer: HP
Product Name: ProLiant DL360 G7
Version: Not Specified
Serial Number: ...
...
Family: ProLiant
```

Test on a Virtual Server in Hetzner (`sudo dmidecode --type system`)
```
System Information
Manufacturer: Hetzner
Product Name: vServer
Version: ...
Serial Number: ...
...
Family: Hetzner_vServer
```

#### lshw