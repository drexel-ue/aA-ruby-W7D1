1. **What is an object?**

**Answer:**
An instance of a class. It's also the root class in ruby (Object). Classes themselves descend from the Object root class.


2. **Explain this ruby idiom: `a ||= b`**

**Answer:**
If the `a` is false then `a = b`. If the `a` side is true then `a` isn't reassigned.

3. **What is unit testing? What is the primary technique when writing a test?**

**Answer:**
Unit testing, simply put, is testing methods -- the smallest unit in object-oriented programming. The primary way to achieve this is to assert that the **actual** result of the method matches an **expected** result.

```rb
RSpec.describe Calculator do
  it "add method adds numbers" do
    calc = Calculator.new
    expect(calc.add(3, 4)).to eq(7)
  end
end
```


### OOP – Parking Lot

### Prompt

Design a parking lot using object-oriented principles.

(Don't spend too much time fleshing out actual methods. Aim to give a
holistic view of which methods exist on each of the classes.)




## Implement DFS

For this problem assume there is a Node class. The node class will take in a value as part of its initialization. You will be monkeypatching the following method:

Write a method `dfs` that does a depth-first search starting at a root node. It takes in a target, and a proc as an argument.
```ruby
n1 = Node.new(1) #making a node with a value of 1

n1.dfs { |node| node.value == 1 } #=> n1 (found a node with value == 1)
```

class Node

def dfs(&prc)

prc ||= Proc.new { |node| node.value == 2 }

return self if prc.call(self)

@children.each do |child_node|

    search_result = child_node.dfs(prc)

    return search_result if search_result

end

nil

end



### Solution

```rb
class Node

  # -- Assume nodes have a value, and a attr_reader on value
  # -- Also, assume there are working parent/child-related methods for Node
  def dfs(, &prc)
    raise "Must give a proc or target" if prc.nil?

    return self if prc.call(self)

    self.children.each do |node|
      result = node.dfs(target, &prc)
      return result if result
    end

    nil
  end
end
```