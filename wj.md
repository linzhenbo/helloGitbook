## 两种实现接口的差异

(隐式)实现接口:通常的实现方式

显示实现接口:在实现的方法前面加上接口的名称,表示只能被*接口类型的实例*调用,而不能被*子类类型的实例*调用

(一个方法可以两种方式都实现) 

 ```c#
//经典例子
/// <summary>
/// 苦B人类
/// </summary>
public class People : IUsaAccount, IChinaAccount
{
    public People(string name, decimal salary)
    {
        this.Name = name;
        this.Salary = salary;
    }

    #region Properties
        public string Name { get; set; }
    public decimal Salary { get; set; }
    #endregion

        #region 隐示实现接口
        public void Compute_Wage()
    {
        Console.WriteLine("统一了，{0}它无论在哪个国家，工资都是{1}", Name, Salary);
    }
    #endregion

        #region 显示实现接口
        #region IUsaAccount 成员

        void IUsaAccount.Compute_Wage()
    {
        Console.WriteLine("在美国，{0}的工资是（原工资{1}*12%的福利）{2}", Name, Salary, Salary * 1.2m);
    }

    #endregion

        #region IChinaAccount 成员

        void IChinaAccount.Compute_Wage()
    {
        Console.WriteLine("在中国，{0}的工资是（原工资{1}－原工资{1}*2%的个税）{2}", Name, Salary, Salary - Salary * 0.02m);
    }
    #endregion


        #endregion
}

//调用
IUsaAccount person1 = new People("zzl", 5000);
person1.Compute_Wage();//6000

IChinaAccount person2 = new People("zzl", 5000);
person2.Compute_Wage();//4900

People person3 = new People("zzl", 5000);
person3.Compute_Wage();//5000

 ```







