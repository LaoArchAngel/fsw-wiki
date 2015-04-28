#### Q: How would you store a list of phone numbers for fast retrieval, like check whether the phone number exists?
#### A:
Use a hastable for storing all phone numbers. This would give us constant time lookup of phone numbers.

##### Q: How would you optimize it for space/storage?
##### A:
Use a tree to store all phone numbers, each digit would be a node in the tree

##### Q: How does that affect performance?
##### A:
Using a tree change the performance to log(10) assuming all phone numbers are 10 digits long, which would still be constant time.

#### Q: How do hashtables work?
#### A:

#### Q: Implement a hashtable?
#### A: 

#### Q: Given an array of positive integers and a product (or sum), please implement a function that finds two numbers in the array whose product (or sum) is the provided value.
#### A: 

```csharp
public void findThem(int[] arr, int sum /* int product */, out int val1, out int val2)
{
   var ht = new Dictionary<int, int>();
   var diff = 0;

   for(int i=0; i <= arr.Length; i++)
   {
      if(!ht.ContainsKey(arr[i]))
         ht.Add(arr[i], arr[j]);
   }

   for(int j=0; j <= arr.Length; j++)
   {
      diff = sum - arr[j]; /* diff = sum / arr[j]; */
      if(ht.ContainsKey(diff))
      {
         val1 = arr[j];
         val2 = diff;
         return;
      }
   }

   val1 = -1;
   val2 = -1;
}
```


#### Q: Implement a min-stack?
#### A:

#### Q: Cleanup file path (UNIX or Windows)? "/home/.././home/./indianajones/../margaret/." must be cleaned up to "/home/margaret", for windows you may assume that the drive letter has been removed and your procedure was passed "\\home\\..\\.\\home\\.\\indianajones\\..\\margaret\\." and it should return "\\home\\margaret".
#### A:

```ruby
def clean_up_path(path)
   path_elements = path.split('/')
   clean_path_elements = []

   path_elements.each { |path_element|
      if path_element == '.'
         continue
      elsif path_element == '.'
         clean_path_elements.pop
      else
         clean_path_elements.push path_element
   }

   return clean_path_elements.join '/'
end
```