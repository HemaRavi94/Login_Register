# Login_Register
import re
def register():
 db=open('database.txt','r')
 email_id = input('enter username\email_id: ')
 password = input('Enter password: ')
 f=[]
 d=[]
 for i in db:
     a,b=i.split(",")
     b=b.strip()
     f.append(a)
     d.append(b)
     data=dict(zip(f,d))
     
 special_char= r'\b[A-Za-z]+[0-9.ft_%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}\b'
 
 if(re.fullmatch(special_char,email_id)):
     print("Valid Email_id")
 else:
     print("Invalid Email_id!! Try again")
 if len(password) < 6:
     print('length should be at least 6')
     register()
 else:
    if len(password) > 20:
          print('length should be not be greater than 8')
          register()
    if not any(char.isdigit() for char in password):
           print('Your Password should have at least one numeral value')
           register()
    if not any(char.isupper() for char in password):
            print('Your Password should have at least one uppercase letter ')
            register()
    if not any(char.islower() for char in password):
               print('Your Password should have at least one lowercase letter')
               register()
    if not any(char in special_char for char in password):
             print('Your Password should have at least one of the special_char ')
             register()
 
 if email_id in f:
         print('email_id exists')
         register()
 else:
   db=open("database.txt","a")
   db.write(email_id+","+password+"\n")
   print('SUCCESS!!')
   register()
def access():
    db=open("database.txt",'r')
    email_id = input('enter username\email_id: ')
    password = input('enter password: ')
    if not len(email_id or password) < 1:
        f=[]
        d=[]
        for i in db:
            a=email_id
            b=password
            f.append(a)
            d.append(b)
            data=dict(zip(f,d))
        try:
            if data[email_id]:
                try:
                    if password == data[email_id]:
                        print("Login Success!!")
                        print("Hi,",email_id)
                    else:
                        print("Password or Username incorrect")
                except:
                    print("username or Password incorrect")
            else:
                print("username doesn't exists")
        except:
            print("username or password doesn't exists")
            
def final(option=None):
    option=input("Login or signup:")
    if option =="Login":
        access()
    elif option == "signup":
        register()
    else:
        print("please enter an option")
         
final()
