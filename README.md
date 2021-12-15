# leetcode
insert intervals


class Solution {
public:
    vector<vector<int>> insert(vector<vector<int>>& intervals, vector<int>& newInterval) {
        
        
        vector<vector<int>> result;
        if(intervals.size()==0){
            result.push_back(newInterval);
            return result;
        }
        else if(intervals.size()==1 && newInterval[0] > intervals[0][1] ){
            result.push_back(intervals[0]);
            result.push_back(newInterval);
            return result;
        }
        else if( newInterval[1] < intervals[0][0] ){
            result.push_back(newInterval);
             for (int i=0; i<intervals.size();i++){
          
            result.push_back(intervals[i]);
             }
            return result;
        }
        int k=0;
        
        int i=0;
        for (; i<intervals.size();i++){
           // cout<<i<<endl;
            result.push_back(intervals[i]);
            
            if( i+1 <intervals.size() &&newInterval[0] > intervals[i][1]&&newInterval[1] < intervals[i+1][0]){
                result.push_back(newInterval);
            }
            else if (i== intervals.size()-1 && newInterval[0] > result[i][1]){
                 result.push_back(newInterval);
            }
            else if(newInterval[0] > result[i][1]){
                
                continue;
                
            }
            else if(newInterval[0] >= result[i][0] && newInterval[1] <= result[i][1]){
               
                i++;
                break;
            }
            else if(newInterval[0] < result[i][0] && newInterval[1] > result[i][1]){
                
                result[i][0]= newInterval[0];
                result[i][1] = newInterval[1];
                i++;
                break;
            }
            else if(newInterval[0] < result[i][0]){
                result[i][0]= newInterval[0];
                i++;
                break;
            }
            else if(newInterval[1] > result[i][1]){
                result[i][1]= newInterval[1];
                i++;
                  
                break;
            }
            
            
        }
 
        k=i-1;
        for (; i<intervals.size();i++){
            if(result[k][1] > intervals[i][0] && result[k][1] > intervals[i][1]){
                continue;
            }
            else if(result[k][1] >= intervals[i][0]){
                result[k][1]= intervals[i][1];
            }
            else{
                result.push_back(intervals[i]);
                k++;
            }
            
        
        }
        return result;
    }
};
