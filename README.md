# coding-interview-questions
These are some of the coding interview questions mainly asked by the interviewwers in India. Feel free to contribute if you find any new question.
#### Questions are asked mainly to write some function which should return values according to their requirement. It shouldn't be too long and very complex. Some time they also ask to create a simple component in react with their desired functionality.

### 1. Write a closure function.
A closure is the combination of a function bundled together (enclosed) with references to its surrounding state (the lexical environment). In other words, a closure gives you access to an outer function's scope from an inner function.

    const outer = (()=>{
      let count = 0
      return (()=>{
        count += 1
        return count
      })
    })()
    
    console.log(outer())
    console.log(outer())
  Here the inner function written from line 8 can access the outer function scope (count) even after the outer function is executed.

### 2. write a function which should take an integer array as argument and return a subset of the array which has the longest sequence of increasing numbers. Example [10, 22, 9, 11, 21, 25, 20, 30, 100] should return [9, 11, 21, 25] as it is the longest subset of numbers which are in the increasing order.


    function longestIncreasingSubset(arr) {
    	let seq = []
      let seqLen = 1
      for(let i=1;i<arr.length; i++){
      	if(arr[i]>arr[i-1]){
        	seqLen++
        } else {
        	seqLen = 1
        }
        seq = seqLen > seq.length ? arr.slice(i-seqLen+1, i+1) : seq
      }
      return seq
    }

    const inputArray = [10, 22, 9, 11, 21, 25, 20, 30, 100];
    console.log("Longest Increasing Subsequence:", longestIncreasingSubset(inputArray));

### 3. Find the second highest number.
    function findSecondHighest(arr) {
      if (arr.length < 2) {
        return "Array must have at least two elements to find the second highest value.";
      }
    
      let firstMax = Number.NEGATIVE_INFINITY;
      let secondMax = Number.NEGATIVE_INFINITY;
    
      for (let i = 0; i < arr.length; i++) {
        if (arr[i] > firstMax) {
          secondMax = firstMax;
          firstMax = arr[i];
        } else if (arr[i] > secondMax && arr[i] < firstMax) {
          secondMax = arr[i];
        }
      }
      if( secondMax == Number.NEGATIVE_INFINITY){
     return "All values in the array are same"
    }
      return secondMax;
    }
    
    const numbers = [12, 5, 8, 10, 15, 18, 18, 17];
    const secondHighest = findSecondHighest(numbers);
    console.log("The second highest value is:", secondHighest);

### 4. Write a component which renders a list and can add new item to the list when clicked on a button.
  In React JS
  
    import React, { useState } from "react";
    
    export default App = () => {
      const employees = [{ name: "Max" }, {name: "Williams" },{ name: "Sean" }];
      const [emp, setEmp] = useState(employees);
      const [inputValue, setInputValue] = useState("");
    
      const handleClick = () => {
        setEmp([...emp, { name: inputValue }]);
        setInputValue("");
      };
    
      return (
        <div style={styles.container}>
          <input type="text" value={inputValue} onChange={(e) => setInputValue(e.target.value)} />
          <div>
            {emp && emp.map(({ name }) => {
                return <div>{name}</div>;
              })}
          </div>
          <button onClick={() => {handleClick()}}>Add</button>
        </div>
      );
    };
    
    const styles = {
      container: {
        textAlign: "center",
      },
    };

.
In React Native

    import React, { useState } from "react";
    import {Pressable,StyleSheet,Text,View,TextInput,FlatList} from "react-native";
    
    function App() {
      const [emp, setEmp] = useState(["David", "John", "James"]);
      const [name, setName] = useState("");
      const handlePress = () => {
        setEmp([...emp, name]);
        setName("");
        console.log(emp);
      };
      return (
        <View style={styles.app}>
          <TextInput placeholder="add name" value={name} style={styles.input}
            onChangeText={(text) => {
              setName(text);
            }}
          />
          {emp && 
            <FlatList data={emp} 
            renderItem={({ item }) => {
                return <Text>{item}</Text>;
              }}
            />
          }
          <Pressable style={styles.button}
            onPress={() => {
              handlePress();
            }}
          >
            <Text style={styles.buttonText}>ADD</Text>
          </Pressable>
        </View>
      );
    }
    
    const styles = StyleSheet.create({
      app: {
        marginHorizontal: "auto",
      },
      input: {
        padding: 10,
      },
      button: {
        backgroundColor: "#2196F3",
      },
      buttonText: {
        color: "#fff",
        padding: 8,
        marginHorizontal: "auto",
      },
    });
    
    export default App;

