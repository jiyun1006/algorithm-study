

```c++

#include <iostream>
#include <queue>
#include <vector>
#include <list>
#include <map>
#include <stack>

using namespace std;


struct Node {
	int data;
	Node* left;
	Node* right;
	Node(int data)
	{
		this->data = data;
		left = NULL;
		right = NULL;
	}

	Node() {}

	
};

void bfs_queue(Node* root)
{
	queue<Node*> q;
	q.push(root);

	while (!q.empty())
	{
		auto node = q.front();
		cout << node->data << " ";
		q.pop();
		if (node->left != NULL)
			q.push(node->left);
		if (node->right != NULL)
			q.push(node->right);
	}
	return;

}


void printPreorder(struct Node* node) {
	if (node == NULL)
		return;
	cout << node->data << " ";
	printPreorder(node->left);
	printPreorder(node->right);
}




int main()
{


	Node* root = new Node(10);
	root->left = new Node(4);
	root->right = new Node(9);
	root->right->left = new Node(2);
	root->right->right = new Node(7);
	root->left->left = new Node(3);
	root->left->right = new Node(1);
	root->left->left->left = new Node(5);
	root->left->left->right = new Node(6);
	
	printPreorder(root);
	cout << endl;
	//bfs_queue(root);
}



```
