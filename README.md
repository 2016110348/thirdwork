# thirdwork
print("作业一：")
let dict = ["yangjian":18,"yupeng":20,"lvkangjia":20,"hekaifu":20]
let maps = dict.map{key,value in key}
print("maps结果：")
print(maps)

let strs = ["test","123","456","yangjian123",",/.$"]
let filters = strs.filter{
    (str) -> Bool in
    return (Int(str) != nil)
}
print("filters结果：")
print(filters)

//let reduces = strs.reduce("", combine:+)
let reduces = strs.reduce(""){
    text,name in "\(text),\(name)"
}
print("reduces结果：")
print(reduces)

print("利用reduce求出数组总和以及数组最大值、最小值:")
let arrays = [1,3,1,1,1,5,1]
print("测试数组：")
print(arrays)
print("求出数组总和：")
print(arrays.reduce(0, +))
print("求出数组最小值：")
print(arrays.reduce(Int.max, min))
print("求出数组最大值：")
print(arrays.reduce(Int.min, max))


func add(a:Int,b:Int) -> Int {
    return a + b
}
func selfAdd(a:Int) -> Int{
    return a + 10
}
func rectangleArea(width:Double,height:Double) -> Double{
    let area = width*height
    return area
}
func triangleArea(bottom:Double,height:Double) -> Double{
    let area = 0.5*bottom*height
    return area
}
print("函数数组结果：")
let funArr:[Any] = [add,rectangleArea,triangleArea,selfAdd]
for (arrIndex,value) in funArr.enumerated(){
    if value is (Int) -> Int {
        print(arrIndex)
    }
}

extension Int{
    func mySqrt() -> Double {
        return sqrt(Double(self))
    }
}
let num = 4
print("扩展int的sqrt方法结果：")
print(num.mySqrt())


func getMaxinum<T: Comparable>(a:T...) -> (T,T) {
//    将第一个值先设为max，min
    var max = a[0]
    var min = a[0]
    
    for item in a {
        if item > max{
            max = item
        }else if item < min{
            min = item
        }
    }
    return (max,min)
}
print("返回最大值最小值对：")
print(getMaxinum(a: 12,4,15,12,0,-153,56))

print("*******************************")
print("作业二：")
enum Gender:String {
    case male
    case female
}
//重载>操作符func >(lhs: Gender, rhs: Gender) -> Bool {
    return lhs.rawValue < rhs.rawValue
}

enum Department {
    case office
    case library
    case classroom
}

protocol SchoolProtocol {
    var department: Department {get set}
    func lenBook()
}

class Person :CustomStringConvertible{
    var firstName : String
    var lastName : String
    var age : Int = 0
    var gender : Gender
    //计算属性
    var fullName : String {
        get {
            return firstName+"."+lastName //返回full name，计算属性
        }
        set (newFullName){
            var name = newFullName.components(separatedBy: ".")
            firstName = name[0]
            lastName = name[1]
        }
    }
    //构造函数
    init(firstName:String, lastName:String, age:Int,gender:Gender){
        self.firstName = firstName
        self.lastName = lastName
        self.age = age
        self.gender = gender
    }
    //便利构造函数
    convenience init(){
        self.init(firstName:"jiang",lastName:"yang",age:18,gender:Gender.male)
    }
    //重写==符号运算
    static func == (a:Person,b:Person)->Bool{
        if(a.firstName == b.firstName&&a.lastName == b.lastName){
            return true
        }else{
            return false
        }
    }
    //重写person类描述
    var description:String {
        return "firstName=\(firstName),lastName=\(lastName),age=\(age),gender=\(gender)" //描述类的属性
    }
    func run() {
        print("person \(self.fullName) is running")
    }
}
//teacher 类
class Teacher:Person, SchoolProtocol{
    var department: Department
    
    func lenBook() {
        print("teacher \(self.fullName) have been lent books")
    }
    
    var title : String
    init(firstName:String,lastName:String,age:Int,title:String,gender:Gender,department:Department){
        self.title = title
        self.department = department
        super.init(firstName:firstName,lastName:lastName,age:age,gender:gender)
    }
    //重写teacher类描述
    override var description:String{
        return "firstName=\(firstName),lastName=\(lastName),age=\(age),gender=\(gender),title=\(title),department:\(department)"
    }
}
//student 类
class Student:Person, SchoolProtocol{
    var department: Department
    
    func lenBook() {
        print("student \(self.fullName) have been lent books")
    }
    
    var stuNo : Int
    init(firstName:String,lastName:String,age:Int,stuNo:Int,gender:Gender,department:Department){
        self.stuNo = stuNo
        self.department = department
        super.init(firstName:firstName,lastName:lastName,age:age,gender:gender)
    }
    //    重写student类描述
    override var description:String{
        return "firstName=\(firstName),lastName=\(lastName),age=\(age),gender=\(gender),stuNo=\(stuNo),department:\(department)"
    }
}
let person1 = Person(firstName:"jun",lastName:"zhang",age:11,gender: Gender.male)
let person2 = Person(firstName:"zhengyu",lastName:"zhang",age:11,gender: Gender.male)
let person3 = Person(firstName:"jun",lastName:"zhang",age:12,gender: Gender.male)
print("person1的信息：")
print(person1)
print("person1与person2比较结果：")
if(person1 == person3){
    print("相等") 
}else{
    print("不相等")
}

//创建实例对象
let teacher1 = Teacher(firstName:"jun",lastName:"zhang",age:12,title:"student", gender:Gender.male,department:Department.office)
let teacher2 = Teacher(firstName: "zhengyu", lastName: "zhang", age: 13, title: "student",gender:Gender.male,department:Department.office)
let student1 = Student(firstName:"jun",lastName:"zhang",age:11,stuNo:2016110352,gender:Gender.male,department:Department.classroom)
let student2 = Student(firstName: "zhengyu", lastName: "zhang", age: 13, stuNo: 2016110353,gender:Gender.male,department:Department.classroom)
print("测试用例输出：")
print(student1)
student1.run()
student1.lenBook()
print(teacher1)
teacher1.run()
teacher1.lenBook()

var personArr = [person1,person2,person3]
var teacherArr = [teacher1,teacher2]
var studentArr = [student1,student2]

var occupation = ["personCount":personArr.count,"teacherCount":studentArr.count,"studentCount":studentArr.count]
print("输出字典中personCount键对应的对象个数：")
print(occupation["personCount"]!)

print("年龄排序结果：")
personArr.sort { return $0.age > $1.age}
print(personArr)

print("姓名排序结果：")
personArr.sort{ return $0.fullName > $1.fullName }
print(personArr)

print("gender+age排序结果：")
personArr.sort{ return ($0.gender > $1.gender) && ($0.age > $1.age) }
print(personArr)
