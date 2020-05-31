# 과제 3 (난이도 상)

https://github.com/udacity/asteroids 에 들어가 해당 리포지토리를 로컬 머신에 클론 받고 다음 과제를 수행해주세요.

## 버그를 유발한 커밋 찾기

asteroids를 실행하면 우주선과 소행성이 나타납니다. 키보드에서 ←와 →를 누르면 우주선이 가리키는 방향이 바뀌고, ↑를 누르면 우주선이 전진합니다. 스페이스 바를 누르면 로켓이 발사되죠. 

index.html 파일을 열고 게임을 직접 실행해 봅시다.

![asteroids-intro](../resources/asteroids-intro.png)

엇! 그런데 에러가 있네요. 스페이스 바에서 손을 떼지 않고 계속 눌러봅시다. 쉼 없이 총알이 발사됩니다. 

![asteroids-bug](../resources/asteroids-bug.png)

이렇게 끊임없이 총알이 발사되면 게임을 금방 깰 수 있어서 안 됩니다. 처음엔 총알이 끊임없이 발사되지 않도록 구현했었는데, 어디선가 총알이 끊임없이 발사되도록 하는 코드가 들어간 것 같네요.

어떤 커밋때문에 버그가 생겼는지 찾아봅시다. 그리고 버그를 수정하려면 어떻게 해야 하는지 적어봅시다.

### 정답

*** 찾는 방법 ***
git checkout HEAD~1를 해주며 어느 단계에서부터 총알이 연속적으로 발사되지 않는지 살펴본다.

*** commit ID ***
25ede83 (25ede836903881848fea811df5b687b59d962da3)
이 커밋에서 game.js파일의 411번째 줄에 있던 코드(this.delayBeforeBullet = 10;)가 지워져 있음. 

*** 수정하기 (푸쉬할 필요가 있으면) ***
원래는 git checkout HEAD~3으로 돌아가서 코드를 수정하고자 했는데 생각처럼 잘 되지 않아서 그냥 마지막 커밋(master가 있는 위치)에서 game.js파일의 424번째 줄에 빠져있던 코드(this.delayBeforeBullet = 10;)를 다시 추가하고 새로 커밋해서 푸쉬했음.
즉, 
1. game.js 코드 수정(line 424에 위의 코드 추가)
2. git add game.js
3. git comment -m 'continuous shooting problem solved'
4. git push

*** 수정하기 (푸쉬할 필요가 없으면) ***
1. git checkout HEAD~3
2. game.js코드 수정(line 411에 위의 코드 추가)
3. git add game.js
4. git commit -m 'a couple missing ends with the ipad version-continuous shooting problem solved'
5. git rebase HEAD master


### 힌트

과제 2를 통해 커밋도 체크아웃 할 수 있다는 것을 배웠습니다. 이전 커밋을 체크하웃하면 타임머신을 타고 과거로 돌아갈 수 있습니다!
