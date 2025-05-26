# Exerc-cio-05-Contagem-de-Pares-Similares-em-rvore
from collections import defaultdict, deque

def similar_pair(n, k, edges):
    tree = defaultdict(list)
    for p, c in edges:
        tree[p].append(c)
    
    count = 0
    
    def dfs(ancestor):
        nonlocal count
        stack = deque([ancestor])
        while stack:
            node = stack.pop()
            if node != ancestor:
                if abs(ancestor - node) <= k:
                    count += 1
            for child in tree.get(node, []):
                stack.append(child)
    
    for node in range(1, n + 1):
        if node in tree:
            dfs(node)
    
    return count

def main():
    
    n, k = map(int, input().split())
    
    
    edges = [tuple(map(int, input().split())) for _ in range(n - 1)]
    
    
    result = similar_pair(n, k, edges)
    print(result)

if __name__ == "__main__":
    main()

