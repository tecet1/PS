```
import queue

def solution(maps):
    x = [1,1,0,0]
    y = [1,0,1,0]
    rows = len(maps)
    columns = len(maps[0])
    visited = [[False for _ in range(columns)] for _ in range(rows)]
    Q = queue.Queue()
    answer = []
    for i in rows:
        for j in columns:
            tsum = 0
            if not visited[i][j]:
                visited[i][j] = true
                Q.put((i,j))
                
                while not Q.empty():
                    cy,cx=q.get()
                    tsum += map[cy][cx]
                    for k in range(4):
                        tx = cx+x[k]
                        ty = cy+y[k]
                    if tx>=0 and tx<columns and ty>=0 and ty<rows and visited[ty][tx] == false:
                        visited[ty][tx] = true
                        Q.put((tx,ty))
                
                answer.append(tsum)

    sort(answer)
    if len(answer)<=0: return -1
    return answer
```