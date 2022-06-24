# Git

## Multi remote

Create a remote:  
`git remote add origin1 <repository url>;`

Create another remote:  
`git remote add origin2 <repository url>;`

Push branch [main] to remote [origin1]:  
git push origin1 main

Pull branch [main] from remote [origin2]:  
git pull origin2 main

## Multi repository in one remote

Add another url:  
`git remote set-url --add origin2 <another repository url>`
