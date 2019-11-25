![CLEVER DATA GIT REPO](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/0-clever-data-github.png "李聪明的数据库")

# 快速收缩所有SQL数据文件
#### Quickly Shrink All SQL Data Files
**发布-日期: 2015年11月19日 (评论)**

![#](images/##############?raw=true "#")

## Contents

- [中文](#中文)
- [English](#English)
- [SQL Logic](#Logic)
- [Build Info](#Build-Info)
- [Author](#Author)
- [License](#License) 


## 中文
下面是一些快速SQL逻辑（logic），它将缩小除了文件流数据文件和FullText数据文件外的所有SQL数据文件。
这将只影响当前处于联机状态的数据库，并忽略当前在数据库镜像中设置为镜像的数据库。

## English
Here’s some quick SQL Logic that will shrink all SQL Data Files but ignore Filestream Data Files, and FullText Data Files.
This will also ONLY affect databases that are currently ONLINE and ignore Databases that are presently set as the Mirror in database mirroring.


---
## Logic
```SQL
use master;
set nocount on
 
declare @shrinkfiles    varchar(max)
set @shrinkfiles    = ''
select  @shrinkfiles    = @shrinkfiles +
'use [' + sd.name + '];' + char(10) +
'dbcc shrinkfile (' + cast(smf.file_id as varchar(3)) + ');' + char(10) from    sys.databases sd
join sys.database_mirroring sdm on sd.database_id = sdm.database_id join sys.master_files smf on sd.database_id = smf.database_id where sd.database_id > 4
and sd.state_desc = 'online'
and sdm.mirroring_role_desc is null
or  sdm.mirroring_role_desc != 'mirror'
and smf.type < 3
order by
sd.database_id asc
exec    (@shrinkfiles)


```



[![WorksEveryTime](https://forthebadge.com/images/badges/60-percent-of-the-time-works-every-time.svg)](https://shitday.de/)

## Build-Info

| Build Quality | Build History |
|--|--|
|<table><tr><td>[![Build-Status](https://ci.appveyor.com/api/projects/status/pjxh5g91jpbh7t84?svg?style=flat-square)](#)</td></tr><tr><td>[![Coverage](https://coveralls.io/repos/github/tygerbytes/ResourceFitness/badge.svg?style=flat-square)](#)</td></tr><tr><td>[![Nuget](https://img.shields.io/nuget/v/TW.Resfit.Core.svg?style=flat-square)](#)</td></tr></table>|<table><tr><td>[![Build history](https://buildstats.info/appveyor/chart/tygerbytes/resourcefitness)](#)</td></tr></table>|

## Author

- **李聪明的数据库 Lee's Clever Data**
- **Mike的数据库宝典 Mikes Database Collection**
- **李聪明的数据库** "Lee Songming"

[![Gist](https://img.shields.io/badge/Gist-李聪明的数据库-<COLOR>.svg)](https://gist.github.com/congmingshuju)
[![Twitter](https://img.shields.io/badge/Twitter-mike的数据库宝典-<COLOR>.svg)](https://twitter.com/mikesdatawork?lang=en)
[![Wordpress](https://img.shields.io/badge/Wordpress-mike的数据库宝典-<COLOR>.svg)](https://mikesdatawork.wordpress.com/)

---
## License
[![LicenseCCSA](https://img.shields.io/badge/License-CreativeCommonsSA-<COLOR>.svg)](https://creativecommons.org/share-your-work/licensing-types-examples/)

![Lee Songming](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/1-clever-data-github.png "李聪明的数据库")

