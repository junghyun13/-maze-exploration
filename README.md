# -maze-exploration
# When N is vertical and M is horizontal and the structure for the maze is given as a two-dimensional array, when 1 is passable and 0 is impassable, adding 1 for each pass is the coordinate of (1, 1) to escape the maze . Find the distance required to travel from to destination (N, M)! N이 수직이고 M이 수평이고 미로의 구조가 2차원 배열로 주어질 때 1은 통과 가능하고 0은 통과 불가능할 때 각 통과마다 1을 더하면 미로를 탈출하기 위한 (1, 1)의 좌표가 됩니다. . 목적지(N,M)까지 이동하는데 필요한 거리를 찾아라!
# c program
#include <stdio.h>
int map[105][105] = {0, }, visit[105][105] = {0, }, dist[105][105], queueX[10005] = {0, }, queueY[10005] = {0, }, N, M;
void BFS(int X, int Y){
	int front=0,rear=1,popX,popY;
	visit[X][Y]=1;
	queueX[0]=X,queueY[0]=Y;
	while(front<rear){
		popX = queueX[front], popY = queueY[front++];
        if(map[popX+1][popY] && !visit[popX+1][popY]) {
            visit[popX+1][popY] = 1;
            dist[popX+1][popY] = dist[popX][popY]+1;
            queueX[rear] = popX+1;
            queueY[rear++] = popY;
        }
        if(map[popX-1][popY] && !visit[popX-1][popY]) {
            visit[popX-1][popY] = 1;
            dist[popX-1][popY] = dist[popX][popY]+1;
            queueX[rear] = popX-1;
            queueY[rear++] = popY;
        }
        if(map[popX][popY+1] && !visit[popX][popY+1]) {
            visit[popX][popY+1] = 1;
            dist[popX][popY+1] = dist[popX][popY]+1;
            queueX[rear] = popX;
            queueY[rear++] = popY+1;
        }
        if(map[popX][popY-1] && !visit[popX][popY-1]) {
            visit[popX][popY-1] = 1;
            dist[popX][popY-1] = dist[popX][popY]+1;
            queueX[rear] = popX;
            queueY[rear++] = popY-1;
        }
	}
}
int main(void){
	int N,M;
	int i,j;
	scanf("%d %d",&N,&M);
	for(i=1;i<=N;i++){
		for(j=0;j<=M;j++){
			scanf("%1d", &map[i][j]);
		}
	}
	dist[1][1] = 1;
    BFS(1, 1);
    printf("%d", dist[N][M]);}
 # python
 n, m = map(int,input().split()) # n, m 입력받기
graph = [] # 2차원 배열로 nxm크기의 미로생성
for _ in range(n):
    graph.append(list(map(int,input().strip())))
#상하좌우
h = [-1, 1, 0, 0]
w = [0, 0, -1, 1]
def bfs(x,y):  #deque를 이용하면 ex)love--> 'l' 'o' 'v' 'e'
    queue = deque()
    queue.append((x,y))
    while queue:
        x, y = queue.popleft()
        for d in range(4): #상하좌우
            xh = x + h[d]
            yw = y + w[d]
            if 0 <= xh < n and 0 <= yw < m:
                if graph[xh][yw] == 1: # 이동할 수 있는 '1'칸을 만족한다면 +1을 해준다.
                    graph[xh][yw] = graph[x][y] + 1
                    queue.append((xh,yw))
    return graph[n-1][m-1] # 목적지n, m의 값 출력
print(bfs(0,0))
#input--> 4 6  101111  101010  101011  111011
#result--> 15
