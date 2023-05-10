如何批量导出微信聊天图片

目前微信只提供多微信终端迁移以及电脑端备份的功能，最终对聊天记录的查看只能在微信端操作。如果你想导出聊天记录通过非微信查看，是行不通的。

但是电脑端的图片是可以批量导出的，只需要做一点点额外的工作。

01 将聊天记录都同步到电脑

首先，为了方便我们导出图片，需要把聊天记录先迁移到电脑端。可以从微信电脑端操作迁移与备份。
或者，微信手机端 设计 -> 聊天记录迁移与备份

注意：如果每天在电脑登录，并勾选同步最近消息，并不能保证所有消息都在电脑端，还是需要聊天记录迁移操作。

02 找到微信存储图片的位置

首先，在设置 -> 文件管理里找到微信文件的默认保存位置。

然后，找到以wxid_开头的文件夹，进入FileStorage，进入MsgAttach，现在进入了所有聊天图片保存的文件夹。这个文件夹又分三层：
第一层，文件夹以32位字母或数字组成，感觉像UUID去掉了横线，每个文件夹基本上代表了一个聊天（私聊或者群聊），不保证一个聊天有两个以上的文件夹。
第二层，文件夹名为Image或者Thumb，分别代表原图和缩略图，如果图片没有点开过，一段时间后无法下载原图，只有缩略图，所以理论上Thumb里图片的数量大于等于Image文件夹内的数量。
第三层，YYYY-MM格式的年月目录，按月份将图片归集。

03 解码

微信存储的图片都是以.dat扩展名结尾，并且其不是单纯的改了文件名，而是对每个字节都做了处理。幸好对于一个文件内的所有字节，异或处理的规律都是相同的。再加上不同图片的头两个字节都是固定的，我们可以根据这两个字节来判断出异或的规律，继而还原整个文件。









