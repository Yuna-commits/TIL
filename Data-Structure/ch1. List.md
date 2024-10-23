# Linked List
## ADT
- 노드 생성(CreateNode)/노드 소멸(DestoryNode)
- 노드 추가(AppendNode)
- 노드 삽입(InsertAfter, InsertNew-Head)
- 노드 삭제(RemoveNode)
- 노드 탐색(GetNode)

## 구성요소
- Head 포인터 : 첫 번째 노드의 주소를 가지는 포인터
- Node
- 데이터 필드 : 각 노드에 저장된 데이터
- 링크 필드 : 다른 노드의 주소가 저장

![image](https://github.com/user-attachments/assets/30eaa8b7-d214-48ff-b1e9-737c6a7773e2)

## 노드 정의

```
typedef int element;
typedef struct{
	element data;
	struct ListNode *link;
}ListNode;
```

## 노드 생성

```
ListNode *Head = (ListNode *)malloc(sizeof(ListNode));
Head->data = 1;
Head->link = NULL;
```

![image](https://github.com/user-attachments/assets/91244595-5279-4387-a657-843bc184548d)

- 맨 마지막 노드의 link를 NULL로 저장하여 리스트의 끝을 알 수 있음

## 노드 삽입

### 첫 번째에 삽입하는 경우

![image](https://github.com/user-attachments/assets/0699fdf0-9baa-45be-8c57-f0b6344a717d)
![image](https://github.com/user-attachments/assets/1c096e97-b62a-4ef6-88a7-c0f339f38c80)

- C 노드를 생성한 뒤, C의 link에 A 노드의 주소를 저장 => C -> A 포인팅
- Head에 C 노드의 주소 저장 => Head -> C 포인팅

```
ListNode* insert_first(ListNode *head,int value)
{
	ListNode *p = (ListNode *)malloc(sizeof(ListNode));
	p->data = value;
	p->link = head;
	head = p;
	return head; 
}
```

### 중간에 삽입하는 경우

![image](https://github.com/user-attachments/assets/3062f22c-70ce-45b8-94d6-9496ed560d07)
![image](https://github.com/user-attachments/assets/01589265-5c80-445f-8d6c-48f27327d201)

- 중간에 삽입하는 경우에는 삽입 위치의 선행 노드 위치가 중요
- Pre 선행 노드의 link에 저장된 D 노드의 주소를 C 노드의 link에 저장 => C -> D 포인팅
- Pre 노드의 link에 C 노드의 주소 저장 => Pre -> C 포인팅

```
ListNode* insert(ListNode *head,ListNode *pre,int value)
{
	ListNode *p = (ListNode *)malloc(sizeof(ListNode));
	p->data = value;
	p->link = pre->link;
	pre->link=p;
	return head;
}
```

## 노드 삭제

### 첫 번째 노드를 삭제하는 경우

![image](https://github.com/user-attachments/assets/2407514e-13af-40b3-8a4b-255f6e9e599d)

- 임시 노드 Removed에 Head 포인터의 값을 저장
- Head를 두 번째 노드로 변경
- Removed를 free시켜 첫번째 노드 삭제

```
ListNode* delete_first(ListNode *head)
{
	ListNode *removed;
	if(head==NULL) return NULL;
	removed = head;
	head = removed->link;
	free(removed);
	return head;
}
```

### 중간 노드를 삭제하는 경우

![image](https://github.com/user-attachments/assets/7587c458-d373-4d2d-9b9e-7e17258b70bb)

- Head 대신 선행 노드를 이용하여 첫 번재 노드 삭제와 같은 방식으로 삭제

```
ListNode* delete(ListNode *head, ListNode *pre)
{
	ListNode *removed; 
	removed = pre->link;
	pre->link = removed->link;
	free(removed);
	return head;
}
```

## 출력

```
void print_list(ListNode *head)
{
	for(ListNode *p= head;p!=NULL;p=p->link) // head 노드 부터 p가 NULL 이 나올때까지 p=p->link를 통해 옆으로 이동
		printf("%d->",p->data); // 각 노드의 값 출력
	printf("NULL\n");
}
```
