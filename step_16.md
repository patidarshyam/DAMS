DAO and DAOImpl
Here i will show you to write the DAO and its implementation. It will be only a sample code. Further logics can be improved.

Inside com.yash.damsapp.dao package create UserDAO interface and add below code.
package com.yash.damsapp.dao;

import com.yash.damsapp.domain.User;

/**
 * This interface will perform operations related with user
 * @author sharma.pankaj
 *
 */
public interface UserDAO {
	
	public void insert(User user);

}


Inside com.yash.damsdb.daoimpl package, create UserDAOImpl class and add below code.
package com.yash.damsapp.daoimpl;

import javax.sql.DataSource;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.jdbc.core.JdbcTemplate;
import org.springframework.stereotype.Repository;
import com.yash.damsapp.dao.UserDAO;
import com.yash.damsapp.domain.User;
@Repository
public class UserDAOImpl implements UserDAO {

	@Autowired
	private DataSource dataSource;
	private JdbcTemplate jdbcTemplate;
	
	@Autowired
	public void setDataSource(DataSource dataSource) {
		this.jdbcTemplate=new JdbcTemplate(dataSource);
	}
	public void insert(User user) {
		String sql="INSERT INTO users (first_name,last_name,contact, email,address,loginname,password) values(?,?,?,?,?,?,?)";
		Object[] params=new Object[]{
				user.getFirst_name(),
				user.getLast_name(),
				user.getContact(),
				user.getEmail(),
				user.getAddress(),
				user.getLoginname(),
				user.getPassword()
		};
		
		jdbcTemplate.update(sql, params);

	}

}
