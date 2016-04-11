---
title: "Facebook�����Τ��R�]���R�M���G���^��^"
output: github_document
---

���R���^�寻���ζK��A��Ƥ��R�϶���2016/01/01��2016/04/11

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

##Ū�����^�寻���θ��
```{r cars}
if (!require('Rfacebook')){
    install.packages("Rfacebook")
    library(Rfacebook)
}

token<-'CAACEdEose0cBAA2FECXxSHFxJxGTHQ9z20wEqQGFd5iW20X2dzrJXeZAaZBZBAlBcZAceKZBZAuNSn0lVaHpdreicNqz4rGA9c3c5V733ZASvsLMiMvGtd2ZCrUjlZAl5ZCZBa9fuHZCPNiZBttHJVGDWFHahZA60ZAi7ZBs3lr8ysEuD8igLd94tF8MdCpaT85vCtHPw8pV8HXZAUJ6nbbHAusJWLU2RiIOLfrhCMGcZD'
totalPage<-NULL
lastDate<-Sys.Date()
DateVectorStr<-as.character(seq(as.Date("2016-01-01"),lastDate,by="5 days"))
for(i in 1:(length(DateVectorStr)-1)){
    tempPage<-getPage("tsaiingwen", token,
                      since = DateVectorStr[i],until = DateVectorStr[i+1])
    totalPage<-rbind(totalPage,tempPage)
}
nrow(totalPage)
```
2016/01/01 �� 2016/04/11�A���^�寻���Τ@�@�� 212 �g�峹



## �C��o��Ƥ��R
���R���^�寻���ΨC�Ѫ��o���
```{r cars}
totalPage$datetime <- as.POSIXct(totalPage$created_time, 
                                 format = "%Y-%m-%dT%H:%M:%S+0000", 
                                 tz = "GMT") 
totalPage$dateTPE <- format(totalPage$datetime, "%Y-%m-%d", 
                            tz = "Asia/Taipei") 
totalPage$weekdays <-weekdays(as.Date(totalPage$dateTPE))
PostCount<-aggregate(id~dateTPE,totalPage,length)
library(knitr)
kable(head(PostCount[order(PostCount$id,decreasing = T),]))
```
2016-01-15(§����)���o��Ƴ̦h

�Ĥ@�g��"���i�ҥi�H�J�A�غاx���A�_�A�ڸ�j�a�]�i�H�@�_�J�A�D��"
�ĤG�g��"�]�\�A�]���ܦ��A�ҥH���`�^�a�A�]���`�Q���a�m�C���O"
�ĤT�g��"�i���ʹ�p�����T���j �u�I�G�x�W�C�@���v�����Ө�̫�"
�ĥ|�g��"�u�I�G�x�W�C�@���v��������A�ڭ̥Τ��Ѫ��ɶ��A�q�n��"
�Ĥ��g��"�i���ʹ�p�����T���j�u��V�ӧQ<U+30FB>�I�G�x�W�v��"
�Ĥ��g��"�ש�A�ڭ̤@�_����o�̤F�C ���A�ڭ̦b�O���A�]�N�O"
�ĤC�g��"�ש�A�ڭ̤@�_����o�̤F�C ���A�ڭ̦b�O���A�]�N�O"

2016-01-11�B2016-01-14�~��

1/11��:

"�ĤT�Ѫ�����j����A���ѱq�Ÿq�X�o�C�o�̬O�A�~�j���A"
"�C�@��ť��d���u�ɺt���t���A�`ı�o�O��ť�L�̯u�ۡB�P"
"�b�o�˪��N�Ѹ̡A���L�M�Ÿq�Ƶ۲ӲӪ��B�A���ݨ��m�˭�"
"��a��B���O�w�w�A�ﭲ�~��a�Ӧw�w�C ����ҳ̪�S�b"
"��a��B���O�w�w�A�ﭲ�~��a�Ӧw�w�C ����ҳ̪�S�b"
"<U+30FB>�u�^�����s<U+30FB>�x�W�n�F�vhttp://goo"

1/14��:

"���ܥx�W�A�@�w�n���\�I�����O���D����a�A�]�O�x�W����"
"�u���@���� ���}�b�ڤ��ΤU �g�O��ꤶ�B �B����B�ڤ�"
"���i�ұ��X�������ϥߩe�A���ȳQ����A�u�Ȥ�����I�q���~"
"�ש�A�ڭ̤@�_����F�o�̡C �|�~�e�����ѡA�ڭ̩Z�M����2"
"�o���]�߶m�˰e�ڪ�����A�ڤ@�����a�ۥ��A�]���A���O"
"�|�~�e�����ѡA�S�����o���ҭˤU�h�C�ڭ̦b���D���|����"
"1/15(��)�u��V����<U+30FB>�I�G�x�W�y�ձ߷|�v��e��"


## �C��Likes�Ƥ��R
���R���^�寻���ΨC�骺�I�g�ƨòέp
```{r cars}
LikesCount<-aggregate(likes_count~datetime,totalPage,mean)
library(knitr)
kable(head(LikesCount[order(LikesCount$likes_count,decreasing = T),]))
```
�ھڸ�ƫ��X�A2016-01-16��"N/A"�I�g�Ƴ̦h

�䦸��2016-01-16��"N/A"
�ĤT��2016-01-16��"���إ���A�X�o�I"
�ĥ|��2016-01-16��"���¦U��ꤺ�~���C��O�̪B�͡A�P�¤j�a���@�ߵ��ԡC"
�Ĥ���2016-01-17��"�U��{�����B�͡A�U��q�����e�����n�B�͡A�����W���ݪ�"
�Ĥ���2016-03-29��"�p�O�w �������|���A�ե��묹�C�o�Ӫ��|�}�F�ܦh�}�A��"




## �C��Comments�Ƥ��R
���R���߭ۯ����ΨC�骺�Q�׼ƨòέp
```{r cars}
CommentsCount<-aggregate(comments_count~datetime,totalPage,mean)
library(knitr)
kable(head(CommentsCount[order(CommentsCount$comments_count,decreasing = T),]))
```

�Ĥ@�h��2016-01-20��"���Ĥ@�����i�Ҥ��`�|�A�����¤j�a�b���|���������A�j"
�ĤG�h��2016-01-21��"�b�G�m�̪F�P�¤j�a�A���m�˭̪��ۮ��A�ߤ�ı�o�S�O�ŷx�C"
�ĤT�h��2016-01-21��"N/A"
�ĥ|�h��2016-01-15��"�i���ʹ�p�����T���j �u�I�G�x�W�C�@���v�����Ө�̫�"
�Ĥ��h��2016-01-20��"���|�����A�٨S���}�l�²���{�A�{�b�ּ̧֪��A�N�O�ש�"
�Ĥ��h��2016-01-16��"N/A"



## �C��Shares�Ƥ��R
���R���߭ۯ����ΨC�骺���ɼƨð��έp
```{r cars}
ShareCount<-aggregate(shares_count~datetime,totalPage,mean)
library(knitr)
kable(head(ShareCount[order(ShareCount$shares_count,decreasing = T),]))
```
�Ĥ@�h��2016-01-16��"�U��{�����B�͡A�U��q�����e�����n�B�͡A�����W���ݪ�"
�ĤG�h��2016-03-29��"�����k�h���@�ʫH�G�q�R�����k�h�A�Q�ߡA�b�q�����e�A�ݨ��z"
�ĤT�h��2016-01-16��"���¦U��ꤺ�~���C��O�̪B�͡A�P�¤j�a���@�ߵ��ԡC"
�ĥ|�h��2016-01-14��"�ש�A�ڭ̤@�_����F�o�̡C �|�~�e�����ѡA�ڭ̩Z�M����"
�Ĥ��h��2016-01-15��"�ש�A�ڭ̤@�_����o�̤F�C ���A�ڭ̦b�O���A�]�N�O"
�Ĥ��h��2016-01-10��"�A���g���}�G�m �G�m �S������ �G�m �û��O�w�R�� �G�m"



