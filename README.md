
1. Descargar el proyecto

$ git clone git@bitbucket.org:orbisunt/orbis-example-training.git

2. Cambiar el repositorio remoto origin por uno de igual nombre en tu cuenta github. (Crear en github el repositorio y enlazarlo)

$ git remote -v
origin  git@bitbucket.org:orbisunt/orbis-example-training.git (fetch)
origin  git@bitbucket.org:orbisunt/orbis-example-training.git (push)


$ git remote set-url origin git@github.com:elmagocarlos/orbis-example-training.git


$ git remote -v
origin  git@github.com:elmagocarlos/orbis-example-training.git (fetch)
origin  git@github.com:elmagocarlos/orbis-example-training.git (push)


3. Subir los cambios a github ¿Qué mensaje aparece?

$ git push origin master
Counting objects: 22, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (14/14), done.
Writing objects: 100% (22/22), 147.22 MiB | 560.00 KiB/s, done.
Total 22 (delta 6), reused 20 (delta 6)
remote: Resolving deltas: 100% (6/6), done.
remote: error: GH001: Large files detected. You may want to try Git Large File Storage - https://git-lfs.github.com.
remote: error: Trace: 8a1c86ee4f6acf937a00235a0d21b572
remote: error: See http://git.io/iEPt8g for more information.
remote: error: File sc.16.tar.gz is 146.81 MB; this exceeds GitHub's file size limit of 100.00 MB
To github.com:elmagocarlos/orbis-example-training.git
 ! [remote rejected] master -> master (pre-receive hook declined)
error: failed to push some refs to 'git@github.com:elmagocarlos/orbis-example-training.git'


4. Ahora el objetivo de esta parte es identificar el archivo más pesado que se encuentra en el repositorio y eliminarlo.

$ git gc

$ git verify-pack -v .git/objects/pack/pack-e121f70e46f7ec3df6d405dfb4895762265c6af7
3bd289d96f8784ba7a3fd793364df80ebaaec1f3 commit 255 162 12
d270f6d507e5a9594183c7a64f112d7e798508fc commit 253 160 174
f3a6dc74d8fd32278c93a5e9d4bbaec4d43c04c5 commit 253 158 334
58f9489718084a6c9338f738d977a1432f20885e commit 254 160 492
cae062d363659c2d679d9abb20198834508c7887 commit 253 158 652
8fe34380ed804c88845fbae21a4fa3269da2e955 commit 254 160 810
4f8272b6df5ac7113f828cdc7bae13433803e584 commit 82 94 970 1 8fe34380ed804c88845fbae21a4fa3269da2e955
7044640436e9b16f956bbdc8d5329d10c8f07d62 blob   766 411 470939
df6d3c8daf78aa146dafb763cfa1dd2bb7c89cf7 blob   11 22 471350 1 7044640436e9b16f956bbdc8d5329d10c8f07d62
7246fb5e4a10799d0f37c296a0de4d89d907aef4 blob   178 121 471372
d4439e170e8e421c24a733c20cad48e7316bb7c8 tree   168 167 471493
f8e21c75ad517d0d7364c7c01e93e91ff1b42605 tree   6 17 471660 1 d4439e170e8e421c24a733c20cad48e7316bb7c8
cfc3322ec593c88d0e4d68c312de3583ca741041 blob   153942735 153904153 471677
b91a766edf815ac4a3528bb85bc684c1fd3800d8 tree   30 45 154375830 1 d4439e170e8e421c24a733c20cad48e7316bb7c8
2c6fd0cd04f3f4fe67b0de6a730089e211eba0c7 tree   6 16 154375875 2 b91a766edf815ac4a3528bb85bc684c1fd3800d8
9d66c8a6f837dc8986951cd514ba99fac5ef729e tree   72 80 154375891
e7ab8dc095b1fa777034e14a6ee421c44eb2f793 tree   37 48 154375971
8da13d8f95633e6466a77fd20b52bc813279be9b tree   37 48 154376019
c2da4ec5d81e77578140f8d74005f1f862afee6d blob   7 20 154376067 1 7044640436e9b16f956bbdc8d5329d10c8f07d62
non delta: 14 objects
chain length = 1: 5 objects
chain length = 2: 1 object
.git/objects/pack/pack-e121f70e46f7ec3df6d405dfb4895762265c6af7.pack: ok

$ git rev-list --objects --all | grep cfc3322ec593c88d0e4d68c312de3583ca741041
cfc3322ec593c88d0e4d68c312de3583ca741041 sc.16.tar.gz

$ git filter-branch -f --index-filter 'git rm --cached --ignore-unmatch sc.16.tar.gz' HEAD
Rewrite f3a6dc74d8fd32278c93a5e9d4bbaec4d43c04c5 (5/8) (3 seconds passed, remaining 1 predicted)    rm 'sc.16.tar.gz'
Rewrite d270f6d507e5a9594183c7a64f112d7e798508fc (5/8) (3 seconds passed, remaining 1 predicted)    rm 'sc.16.tar.gz'
Rewrite 8cac391b514f671eadc0af13a33a7fa092f7406c (7/8) (4 seconds passed, remaining 0 predicted)
Ref 'refs/heads/master' was rewritten


5. Subir los cambios


$ git push origin master
Counting objects: 19, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (14/14), done.
Writing objects: 100% (19/19), 461.02 KiB | 4.12 MiB/s, done.
Total 19 (delta 5), reused 12 (delta 3)
remote: Resolving deltas: 100% (5/5), done.
remote:
remote: Create a pull request for 'master' on GitHub by visiting:
remote:      https://github.com/elmagocarlos/orbis-example-training/pull/new/master
remote:
To github.com:elmagocarlos/orbis-example-training.git
 * [new branch]      master -> master



