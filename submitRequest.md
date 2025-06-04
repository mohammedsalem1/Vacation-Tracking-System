 // use-case Manage Time //
 ********* create new vacation ******
 start 
   function createLeaveRequest(employee , dataRange , category_name)
      validationData = {employee , dataRange , category_name}
      if !validationData return "The data is not correct"
      leaveRequest =  {employee , dataRange , category_name}
      updateEmployeeleaveRequest()
      SaveLeaveRequestInDB()
      NotifyManager()
      if Manger's proved
  end  