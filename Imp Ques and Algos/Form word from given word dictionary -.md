![[WhatsApp Image 2023-07-19 at 10.38.54 AM.jpeg|800]]

```C++
#include <iostream>
#include <string>
#include <unordered_set>
#include <vector>

using namespace std;
bool canFormWordHelper(const string &word,
                       const unordered_set<string> &wordDict,
                       unordered_set<string> &memo) {
    if (word.empty()) {
        return true;
    }

    if (memo.find(word) != memo.end()) {
        return false;
    }

    for (int i = 1; i <= word.length(); ++i) {
        string prefix = word.substr(0, i);
        if (wordDict.find(prefix) != wordDict.end()) {
            string suffix = word.substr(i);
            if (canFormWordHelper(suffix, wordDict, memo)) {
                return true;
            }
        }
    }

    memo.insert(word);
    return false;
}

bool canFormWord(const string &word, const vector<string> &wordDict) {
    unordered_set<string> wordSet(wordDict.begin(), wordDict.end());
    unordered_set<string> memo;
    return canFormWordHelper(word, wordSet, memo);
}

int main() {
    string word = "penappleapple";
    vector<string> wordDict = {"pen", "apple", "pear", "pieapple"};

    if (canFormWord(word, wordDict)) {
        cout << "The word \"" << word
             << "\" can be formed from the word dictionary." << endl;
    } else {
        cout << "The word \"" << word
             << "\" cannot be formed from the word dictionary." << endl;
    }

    return 0;
}

```

