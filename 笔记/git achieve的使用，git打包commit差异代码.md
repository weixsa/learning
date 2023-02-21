参考blog
https://blog.csdn.net/weixin_38451161/article/details/86509660

1： 导出最后一次提交修改过的文件
git archive -o ../updated.zip HEAD $(git diff --name-only HEAD^)

2： 导出两次提交之间修改过的文件
git archive -o ../latest.zip NEW_COMMIT_ID_HERE $(git diff --name-only OLD_COMMIT_ID_HERE NEW_COMMIT_ID_HERE)


以上两种场景可以会输出以下这种异常
fatal: pathspec 'xxxxxx/xx/xxxx/model/CommonResponse.java' did not match any files
问题根因可能是：执行命令所在的路径可能不对，要在项目的根路径下

使用这个命令查看两次提交之间的变更文件路径
git diff --diff-filter=ACMR NEW_COMMIT_ID_HERE OLD_COMMIT_ID_HERE  --name-only

然后在使用这个命名进行打包，或者上边那个命令
git diff --diff-filter=ACMR HEAD^ --name-only | xargs tar -czvf 文件导出路径
