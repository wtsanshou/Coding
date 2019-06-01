# LC355. Design Twitter

### LeetCode

## Question

Design a simplified version of Twitter where users can post tweets, follow/unfollow another user and is able to see the 10 most recent tweets in the user's news feed. Your design should support the following methods:

1.	postTweet(userId, tweetId): Compose a new tweet.
2.	getNewsFeed(userId): Retrieve the 10 most recent tweet ids in the user's news feed. Each item in the news feed must be posted by users who the user followed or by the user herself. Tweets must be ordered from most recent to least recent.
3.	follow(followerId, followeeId): Follower follows a followee.
4.	unfollow(followerId, followeeId): Follower unfollows a followee.

**Example:**

```
Twitter twitter = new Twitter();

// User 1 posts a new tweet (id = 5).
twitter.postTweet(1, 5);

// User 1's news feed should return a list with 1 tweet id -> [5].
twitter.getNewsFeed(1);

// User 1 follows user 2.
twitter.follow(1, 2);

// User 2 posts a new tweet (id = 6).
twitter.postTweet(2, 6);

// User 1's news feed should return a list with 2 tweet ids -> [6, 5].
// Tweet id 6 should precede tweet id 5 because it is posted after tweet id 5.
twitter.getNewsFeed(1);

// User 1 unfollows user 2.
twitter.unfollow(1, 2);

// User 1's news feed should return a list with 1 tweet id -> [5],
// since user 1 is no longer following user 2.
twitter.getNewsFeed(1);
```

## Solutions

### Solution 1

* C++
```
class Twitter {
private:
    unordered_map<int, unordered_set<int>> followeree; // follower, followees
    unordered_map<int, map<int, int>> tweetters; // userId, timestamp, tweetId
    long long tweetNum;
public:
    /** Initialize your data structure here. */
    Twitter() {
        tweetNum = 0;
    }
    
    /** Compose a new tweet. */
    void postTweet(int userId, int tweetId) {
        tweetters[userId][tweetNum++] = tweetId;
        follow(userId, userId); // if user post a tweet, follow himself
    }
    
    /** Retrieve the 10 most recent tweet ids in the user's news feed. Each item in the news feed must be posted by users who the user followed or by the user herself. Tweets must be ordered from most recent to least recent. */
    vector<int> getNewsFeed(int userId) {
        vector<int> res;
        map<int, int> top10; //this is an ordered map
        for(auto followee : followeree[userId])
        {
            for(auto tweet=tweetters[followee].rbegin(); tweet!=tweetters[followee].rend(); ++tweet)
            {
                if(top10.size()==10 && top10.begin()->first > tweet->first) break;
                top10[tweet->first] = tweet->second;
                if(top10.size()>10) top10.erase(top10.begin());
            }
        }
        for(auto top=top10.rbegin(); top!=top10.rend(); ++top)
            res.push_back(top->second);
        return res;
    }
    
    /** Follower follows a followee. If the operation is invalid, it should be a no-op. */
    void follow(int followerId, int followeeId) {
        followeree[followerId].insert(followeeId);
    }
    
    /** Follower unfollows a followee. If the operation is invalid, it should be a no-op. */
    void unfollow(int followerId, int followeeId) {
        if(followerId != followeeId)
            followeree[followerId].erase(followeeId);
    }
};

/**
 * Your Twitter object will be instantiated and called as such:
 * Twitter obj = new Twitter();
 * obj.postTweet(userId,tweetId);
 * vector<int> param_2 = obj.getNewsFeed(userId);
 * obj.follow(followerId,followeeId);
 * obj.unfollow(followerId,followeeId);
 */
```

Using `tweetNum` to identify the timestamp of each post.

Using a map to store the posts for each user.

Using a map to map the user to their followee (Note the user is followee of herself).

The key is the `getNewsFeed`. Put all posts of the user's followee into an ordered map. Keep the sive of the map be less or equal than 10.

**postTweet Complexity:**

* **worst-case time complexity:** `O(1)`.
* **worst-case space complexity:** `O(1)`.

**getNewsFeed Complexity:**

* **worst-case time complexity:** `O(t)` where `t` is the number of tweets.
* **worst-case space complexity:** `O(1)`.

**follow Complexity:**

* **worst-case time complexity:** `O(1)`.
* **worst-case space complexity:** `O(1)`.

**unfollow Complexity:**

* **worst-case time complexity:** `O(1)`.
* **worst-case space complexity:** `O(1)`.

