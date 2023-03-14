# Distance-of-nearest-cell-having-1
Given a binary grid of n*m. Find the distance of the nearest 1 in the grid for each cell.
The distance is calculated as |i1  - i2| + |j1 - j2|, where i1, j1 are the row number and column number of the current cell, and i2, j2 are the row number and column number of the nearest cell having value 1.
 

Example 1:

Input: grid = {{0,1,1,0},{1,1,0,0},{0,0,1,1}}
Output: {{1,0,0,1},{0,0,1,1},{1,1,0,0}}
Explanation: The grid is-
0 1 1 0 
1 1 0 0 
0 0 1 1 
0's at (0,0), (0,3), (1,2), (1,3), (2,0) and
(2,1) are at a distance of 1 from 1's at (0,1),
(0,2), (0,2), (2,3), (1,0) and (1,1)
respectively.


class Solution
{
    //Function to find distance of nearest 1 in the grid for each cell.
    class Pair
    {
        int x,y;
        Pair(int x,int y)
        {
            this.x=x;
            this.y=y;
        }
    }
    public boolean isValid(int x,int y,int[][] grid)
    {
     return x>-1 && x<grid.length &&  y>-1 && y<grid[0].length;  
    }
    public int[][] nearest(int[][] grid)
    {
       Queue<Pair> cord=new LinkedList<>();
       int[][] ans=new int[grid.length][grid[0].length];
       for(int i=0;i<grid.length;i++)
       {
           for(int j=0;j<grid[0].length;j++)
           {
               if(grid[i][j]==1)
               {
                   ans[i][j]=0;
                   cord.add(new Pair(i,j));
               }
               else
               {
                   ans[i][j]=Integer.MAX_VALUE;
               }
           }
       }
       while(!cord.isEmpty())
       {
           int x=cord.peek().x;
           int y=cord.peek().y;
           
           if(isValid(x-1,y,grid) && ans[x-1][y]>ans[x][y]+1)
           {
            ans[x-1][y]=ans[x][y]+1; 
            cord.add(new Pair(x-1,y));
           }
           if(isValid(x+1,y,grid) && ans[x+1][y]>ans[x][y]+1)
           {
            ans[x+1][y]=ans[x][y]+1;
            cord.add(new Pair(x+1,y));
           }
           if(isValid(x,y-1,grid) && ans[x][y-1]>ans[x][y]+1)
           {
              ans[x][y-1]=ans[x][y]+1;
               cord.add(new Pair(x,y-1));
           }
           if(isValid(x,y+1,grid) && ans[x][y+1]>ans[x][y]+1)
           {
               ans[x][y+1]=ans[x][y]+1;
               cord.add(new Pair(x,y+1));
           }
           cord.remove();
       }
           return ans;
       
    }
}
