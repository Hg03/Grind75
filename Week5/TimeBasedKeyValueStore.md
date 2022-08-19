[Problem Statement](https://leetcode.com/time-based-key-value-store/)

[Refer It]()https://youtu.be/fu2cD_6E8Hw)

```cpp
class TimeMap {
private:
    unordered_map<string, vector<pair<int, string>>> timeMap;
public:
    TimeMap() {
        
    }
    
    void set(string key, string value, int timestamp) {
        timeMap[key].push_back(make_pair(timestamp, value));
    }

    string get(string key, int timestamp) {
        // map is sorted by key, perform a binary search
        auto it = timeMap.find(key);
        if (it == timeMap.end())
        {
            return "";
        }
        auto &v = it->second;
        int left = 0, right = v.size() - 1;
        while (left <= right)
        {
            int mid = left + (right - left) / 2;
            if (v[mid].first > timestamp)
            {
                right = mid - 1;
            }
            else if (v[mid].first < timestamp)
            {
                left = mid + 1;
            }
            else
            {
                right = mid;
                break;
            }
        }
        if (right < 0) return "";
        return v[right].second;
    }
};

/**
 * Your TimeMap object will be instantiated and called as such:
 * TimeMap* obj = new TimeMap();
 * obj->set(key,value,timestamp);
 * string param_2 = obj->get(key,timestamp);
 */
```
