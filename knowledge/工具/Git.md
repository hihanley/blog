# Git

## Multi remote

Create a remote:  
`git remote add origin1 <repository url>;`

Create another remote:  
`git remote add origin2 <repository url>;`

Push branch [main] to remote [origin1]:  
`git push origin1 main`

Pull branch [main] from remote [origin2]:  
`git pull origin2 main`

## Multi repository in one remote

Add another url:  
`git remote set-url --add origin2 <another repository url>`

## GitHub 多用户 SSH config 配置

```text
Host github
  HostName github.com
  User git
  PreferredAuthentications publickey
  IdentityFile ~/.ssh/file_a

Host github-other.com
  HostName github.com
  PreferredAuthentications publickey
  IdentityFile ~/.ssh/file_b

# eg：github:user/project.git
# eg：git@github-other.com:user/project.git
```
