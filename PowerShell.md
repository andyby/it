# PowerShell Notes

https://www.varonis.com/blog/powershell-array/

$t = @{n='t'; e={ $_.group[0].timewindow} } 

$d = @{n='d'; e={ $_.group[0].processname} }

$c = @{n='c'; e = "Count"}
e = "Count"

./3.ps1 | Group-Object timewindow,devicename,processname |
Select-Object $t, $d, $c | Sort-Object 't','c' | less

# ./3.ps1 | Group-Object timewindow,devicename,processname |
# Select-Object $t, $d, $c | Sort-Object @{e='t'},@{e='c'; descending=$true} | less
```
./3.ps1 | Group-Object timeWindow 
	| Select-Object @{Name='nName'; expression='name'},
			@{name='xxx'; expression={ $_.group.processName | sort-object -Descending }}

sort-object @{Expression='columnName'; descending=fase},@{...2nd...}
$data = @(

	[pscustomobject]@{FirstName='Kevin';LastName='Marquette'}
	[pscustomobject]@{FirstName='John'; LastName='Doe'}

)
PS /home> ./3.ps1 | Group-Object processName | Sort-Object count -Descending | Select-Object count,name -First 10

```

### sort hashtable/object
```
$hash.GetEnumerator() | Sort-Object -Property Key -Descending
$hash.GetEnumerator() | Sort-Object @{ Expression='Value'; Descending=$false }

$hash.GetEnumerator() | Sort-Object { $_.Value.v } -Descending | ConvertTo-Json
```
## cmdlet get info

-First 10
get the first 10 item
```
PS /> Get-ChildItem                               

    Directory: /

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
l----           9/21/2021  4:48 PM                bin -> /usr/bin
d----           4/15/2020 11:09 AM                boot
d----          10/10/2021  1:54 AM                dev
d----          10/10/2021  1:54 AM                etc
d----           4/15/2020 11:09 AM                home
l----           9/21/2021  4:48 PM                lib -> /usr/lib
l----           9/21/2021  4:48 PM                lib32 -> /usr/lib32
l----           9/21/2021  4:48 PM                lib64 -> /usr/lib64
l----           9/21/2021  4:48 PM                libx32 -> /usr/libx32
d----           9/21/2021  4:48 PM                media
d----           9/21/2021  4:48 PM                mnt
d----           10/5/2021  1:21 AM                opt
d-r--          10/10/2021  1:54 AM                proc
d----           10/5/2021  1:21 AM                root
d----           9/21/2021  5:00 PM                run
l----           9/21/2021  4:48 PM                sbin -> /usr/sbin
d----           9/21/2021  4:48 PM                srv
d-r--            3/4/2021  6:42 AM                sys
d----          10/10/2021  1:54 AM                tmp
d----           9/21/2021  4:48 PM                usr
d----           9/21/2021  5:00 PM                var
```

## filter item
```
PS /> Get-ChildItem | Select-Object -Property name    

Name
----
bin
boot
dev
etc
home
lib
lib32
lib64
libx32
media
mnt
opt
proc
root
run
sbin
srv
sys
tmp
usr
var
```

## sort item
```
PS /> Get-ChildItem | Sort-Object mode -Descending

    Directory: /

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d----           9/21/2021  4:48 PM                mnt
d----          10/10/2021  1:54 AM                tmp
d----           9/21/2021  4:48 PM                srv
d----           9/21/2021  5:00 PM                run
d----           10/5/2021  1:21 AM                root
d----           10/5/2021  1:21 AM                opt
d----           9/21/2021  4:48 PM                usr
d----           9/21/2021  4:48 PM                media
d----           9/21/2021  5:00 PM                var
d----           4/15/2020 11:09 AM                home
d----          10/10/2021  1:54 AM                etc
d----          10/10/2021  1:54 AM                dev
d----           4/15/2020 11:09 AM                boot
d-r--          10/10/2021  1:54 AM                proc
d-r--            3/4/2021  6:42 AM                sys
l----           9/21/2021  4:48 PM                lib64 -> /usr/lib64
l----           9/21/2021  4:48 PM                lib32 -> /usr/lib32
l----           9/21/2021  4:48 PM                lib -> /usr/lib
l----           9/21/2021  4:48 PM                sbin -> /usr/sbin
l----           9/21/2021  4:48 PM                libx32 -> /usr/libx32
l----           9/21/2021  4:48 PM                bin -> /usr/bin
```
