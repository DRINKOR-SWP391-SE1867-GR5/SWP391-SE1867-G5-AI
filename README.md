 public User loginUser(String email, String password) {
        String query = "SELECT * FROM [User] WHERE Email = ? AND Password = ?";
        try {
            ps = conn.prepareStatement(query);
            ps.setString(1, email);
            ps.setString(2, password);
            rs = ps.executeQuery();
            if (rs.next()) {
                User user = new User();
                user.setId(rs.getInt("ID"));
                user.setEmail(rs.getString("Email"));
                user.setPassword(rs.getString("Password"));
                user.setFullname(rs.getString("Fullname"));
                user.setGender(rs.getString("Gender"));
                user.setAddress(rs.getString("Address"));
                user.setPhone(rs.getString("Phone"));
                user.setIsDeleted(rs.getBoolean("IsDeleted"));
                user.setCreatedAt(rs.getDate("CreatedAt"));
                user.setCreatedBy(rs.getInt("CreatedBy"));
                user.setAvatar(rs.getString("Avatar"));
                user.setChangeHistory(rs.getString("ChangeHistory"));
                return user;
            }
        } catch (SQLException e) {
            Logger.getLogger(UserDAO.class.getName()).log(Level.SEVERE, null, e);
        } finally {
            closeResources();
        }
        return null;
    }

    private void closeResources() {
        
    }
}
