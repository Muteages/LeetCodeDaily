# Replace Words

https://leetcode.com/problems/replace-words

In English, we have a concept called root, which can be followed by some other word to form another longer word - let's call this word derivative. For example, when the root "help" is followed by the word "ful", we can form a derivative "helpful".

Given a dictionary consisting of many roots and a sentence consisting of words separated by spaces, replace all the derivatives in the sentence with the root forming it. If a derivative can be replaced by more than one root, replace it with the root that has the shortest length.

Return the sentence after the replacement.


## Approach 1

Brute force. Modify the string in place.
``` C++
    string replaceWords(vector<string>& dictionary, string sentence) {
        std::unordered_set<std::string> us(dictionary.begin(), dictionary.end());
        size_t left = 0, right = 0;
        std::string temp{};
        while (right < sentence.length())
        {
            right = sentence.find(' ', left);
            temp = sentence.substr(left, right - left);
            std::string prefix{};
            int i = 0;
            for (; i < temp.size(); i++)
            {
                prefix += temp[i];
                if (us.count(prefix))
                {
                    sentence.replace(left, right - left, prefix);
                    break;
                }
            }
            left = left + i + 1;
        }
        return sentence;
    }
```

## Approach 2

Brute force. Create a new string

``` C++
    string replaceWords(vector<string>& dictionary, string sentence) {
        std::unordered_set<std::string> us(dictionary.begin(), dictionary.end());
        std::stringstream ss(sentence);
        std::string curr{}, ans{};
        while (ss >> curr)
        {
            std::string prefix{};
            for (char ch : curr)
            {
                prefix += ch;
                if (us.count(prefix))
                {
                    break;
                }
            }
            ans += prefix + " ";
        }
        ans.pop_back();
        return ans;
    }
```

## Approach 3

Trie

``` C++
    string replaceWords(vector<string>& dictionary, string sentence) {
        Trie trie;
        for (const auto& word : dictionary)
        {
            trie.insert(word);
        }

        std::string ans{}, word{};
        std::stringstream ss(sentence);
        while (ss >> word)
        {
            ans += trie.findPrefix(word);
            ans += " ";
        }

        ans.pop_back();
        return ans;
    }

    struct Trie
    {
        Trie()
        {
            for (int i = 0; i < 26; i++)
            {
                children[i] = nullptr;
            }
            isEnd = false;
        }

        ~Trie()
        {
            for (int i = 0; i < 26; i++)
            {
                delete children[i];
                children[i] = nullptr;
            }
        }

        void insert(const std::string& word)
        {
            Trie* node = this;
            for (char ch : word)
            {
                int i = ch - 'a';
                if (!node->children[i])
                {
                    node->children[i] = new Trie();
                }
                node = node->children[i];
            }
            node->isEnd = true;
        }

        std::string findPrefix(const std::string& word)
        {
            Trie* node = this;
            std::string prefix{};
            for (char ch : word)
            {
                int i = ch - 'a';
                if (!node->children[i])
                {
                    return word;
                }
                node = node->children[i];
                prefix += ch;
                if (node->isEnd)
                {
                    return prefix;
                }
            }
            return word;
        }

        Trie* children[26];
        bool isEnd;
    };
```