
# Time complexity of BFS graph


pseudo-code 

                    q.push(start); 
                    while (!q.empty())  
                    {  
                        int u = q.front();  // get the next vertex in the queue  
                        q.pop();  // remove the vertex from the queue  
                  
                        order.push_back(u);  // add the vertex to the traversal order  
                  
                        // add all the unvisited neighbors of u to the queue  
                        for (int v : adj_list[u])  
                        {  
                            if (!visited[v])  
                            {  
                                q.push(v);  
                                visited[v] = true;  
                            }  
                        }  
                    }  



the while loop runs for all vertices - **O(V)**

and the internal for loop runs for i)UndDirected graph = O(2E)

therefore total = **O(V+2E))**

ii)Directed graph = O(E)

therefore total = **O(V+E)**

**Space complexity is O(V) as we use queue data structure**


# Djikstra 

for time complexity watch 

**https://www.youtube.com/watch?v=3dINsjyfooY&list=PLgUwDviBIf0oE3gA41TKO2H5bHpPd7fzn&index=34**

O(Elog(v))
