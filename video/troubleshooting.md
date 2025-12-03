# Troubleshooting

> Panduan menyelesaikan masalah biasa laman web UiTM

## Lupa Password

Tutorial ini merangkumi masalah-masalah yang kerap dihadapi oleh webmaster dan cara mengatasinya.

---

## 🎬 Tutorial Video

### Video 1: Common Issues & Quick Fixes

**Durasi:** 20 minit

Masalah biasa:

- Website tidak boleh diakses
- Imej tidak keluar
- Broken links
- Layout rosak
- Forms tidak berfungsi

<div class="video-container">
  <iframe width="560" height="315" src="https://www.youtube.com/embed/VIDEO_ID" frameborder="0" allowfullscreen></iframe>
</div>

> 📹 **[Tonton di YouTube](#)** (Coming soon)

---

### Video 2: Debug Mode & Error Logs

**Durasi:** 18 minit

Belajar:

- Enable debug mode
- Reading error logs
- PHP error messages
- Database errors
- JavaScript console errors

<div class="video-container">
  <iframe width="560" height="315" src="https://www.youtube.com/embed/VIDEO_ID" frameborder="0" allowfullscreen></iframe>
</div>

> 📹 **[Tonton di YouTube](#)** (Coming soon)

---

### Video 3: Extension/Plugin Conflicts

**Durasi:** 15 minit

Menyelesaikan:

- Identifying conflicts
- Disable problematic extensions
- Finding alternatives
- Testing compatibility

<div class="video-container">
  <iframe width="560" height="315" src="https://www.youtube.com/embed/VIDEO_ID" frameborder="0" allowfullscreen></iframe>
</div>

> 📹 **[Tonton di YouTube](#)** (Coming soon)

---

## 🚨 Masalah Biasa & Penyelesaian

### 1. Laman Web Tidak Boleh Diakses

#### Gejala:

- "Site can't be reached"
- "Connection timed out"
- "This site can't provide a secure connection"

#### Penyelesaian:

**A. Check Server Status**

```powershell
# Ping server
ping yoursite.uitm.edu.my

# Check if port 80/443 is open
Test-NetConnection yoursite.uitm.edu.my -Port 80
Test-NetConnection yoursite.uitm.edu.my -Port 443
```

**B. Check DNS**

- Verify domain DNS settings
- Clear DNS cache
- Contact ITM if DNS issue

**C. Check SSL Certificate**

- Ensure SSL certificate valid
- Check expiry date
- Renew if necessary

---

### 2. White Screen / Blank Page

#### Penyebab:

- PHP errors
- Memory limit exceeded
- Plugin conflicts

#### Penyelesaian:

**A. Enable Error Reporting**

```php
// Add to top of index.php temporarily
error_reporting(E_ALL);
ini_set('display_errors', 1);
```

**B. Increase Memory Limit**

```php
// In configuration.php or wp-config.php
ini_set('memory_limit', '256M');
```

**C. Disable Extensions**

- Rename plugins/extensions folder
- Access admin panel
- Enable one by one to find culprit

---

### 3. Imej Tidak Keluar / Broken Images

#### Penyelesaian:

**A. Check File Path**

```html
<!-- Ensure correct path -->
✅ <img src="/images/photo.jpg" /> ❌ <img src="C:\local\path\photo.jpg" />
```

**B. Check File Permissions**

```bash
# Should be 644 for files, 755 for directories
chmod 644 image.jpg
chmod 755 images/
```

**C. Check File Exists**

- Verify file uploaded
- Check filename spelling (case-sensitive)
- Check file extension

**D. Check .htaccess**

- Hotlink protection might block images
- Review rewrite rules

---

### 4. Layout Rosak / Broken Layout

#### Penyebab:

- CSS not loading
- JavaScript errors
- Template issues
- Cache problems

#### Penyelesaian:

**A. Clear Cache**

```
Admin Panel → System → Clear Cache
Browser: Ctrl + Shift + Delete
```

**B. Check CSS/JS Files**

- View page source
- Check if CSS/JS files load
- Look for 404 errors in browser console

**C. Check Template**

- Switch to default template
- If works, template issue
- Contact template developer

**D. Disable JavaScript**

- Check if JavaScript error
- Open browser console (F12)
- Fix JavaScript errors

---

### 5. Login Tidak Berfungsi

#### Masalah:

- Lupa password
- Account locked
- Session issues

#### Penyelesaian:

**A. Reset Password**

- Use "Forgot Password" function
- Or reset via database:

```sql
-- Joomla password reset
UPDATE uitm_users
SET password = MD5('newpassword')
WHERE username = 'admin';
```

**B. Check Session Configuration**

```php
// Check session handler in configuration
'sess_handler' => 'database' // or 'filesystem'
```

**C. Clear Sessions**

```sql
-- Clear session table
TRUNCATE TABLE uitm_session;
```

---

### 6. Slow Website Performance

#### Diagnosis:

**A. Check Server Resources**

```powershell
# Check CPU and memory usage
Get-Process | Sort-Object CPU -Descending | Select-Object -First 10
```

**B. Use Performance Tools**

- Google PageSpeed Insights
- GTmetrix
- Pingdom

#### Penyelesaian:

**A. Optimize Images**

- Compress large images
- Use correct dimensions
- Lazy loading

**B. Enable Caching**

- Browser caching
- Server-side caching
- CDN caching

**C. Minify Assets**

- Minify CSS
- Minify JavaScript
- Combine files

**D. Check Database**

```sql
-- Optimize tables
OPTIMIZE TABLE uitm_content;
OPTIMIZE TABLE uitm_menu;
```

---

### 7. Forms Tidak Berfungsi

#### Penyebab:

- Email configuration
- CAPTCHA issues
- JavaScript errors
- PHP mail() disabled

#### Penyelesaian:

**A. Test Email Configuration**

```php
// Test PHP mail
mail('test@uitm.edu.my', 'Test', 'This is a test');
```

**B. Check SMTP Settings**

- Use SMTP instead of PHP mail
- Verify SMTP credentials
- Check firewall/port blocking

**C. CAPTCHA**

- Verify reCAPTCHA keys
- Check site domain matches

---

### 8. Database Connection Error

#### Gejala:

- "Error establishing database connection"
- "Database connection failed"

#### Penyelesaian:

**A. Check Database Credentials**

```php
// In configuration.php
public $host = 'localhost';
public $user = 'dbuser';
public $password = 'dbpass';
public $db = 'dbname';
```

**B. Check Database Server**

```powershell
# Test MySQL connection
mysql -h localhost -u dbuser -p
```

**C. Repair Database**

```sql
REPAIR TABLE table_name;
```

---

### 9. 404 Error untuk Menu Items

#### Penyebab:

- .htaccess missing
- URL rewrite not enabled
- Incorrect base URL

#### Penyelesaian:

**A. Check .htaccess Exists**

- Restore from backup if missing
- Check file permissions

**B. Enable mod_rewrite**

```apache
# In .htaccess
RewriteEngine On
```

**C. Check Configuration**

```php
// Set correct Live Site URL
public $live_site = 'https://yoursite.uitm.edu.my';
```

---

### 10. After Update Issues

#### Masalah:

- Site broke after updating
- Extensions not compatible

#### Penyelesaian:

**A. Rollback**

- Restore from backup before update
- Revert to previous version

**B. Check Extension Compatibility**

- Update all extensions
- Disable incompatible ones
- Find alternatives

**C. Clear Cache**

- System cache
- Browser cache
- OPcache (if enabled)

---

## 🔍 Debug Checklist

### Basic Checks:

- [ ] Check error logs
- [ ] Enable debug mode
- [ ] Clear cache
- [ ] Check file permissions
- [ ] Verify database connection
- [ ] Check server status

### Browser Checks:

- [ ] Try different browser
- [ ] Clear browser cache
- [ ] Disable browser extensions
- [ ] Check console for errors (F12)
- [ ] Test in incognito mode

### Server Checks:

- [ ] Check disk space
- [ ] Check memory usage
- [ ] Check PHP version
- [ ] Check MySQL status
- [ ] Review error logs

---

## 📝 Error Log Locations

### Joomla:

```
/logs/error.php
```

### PHP Error Log:

```
/var/log/php_errors.log (Linux)
C:\xampp\php\logs\php_error_log (Windows)
```

### Apache Error Log:

```
/var/log/apache2/error.log (Linux)
C:\xampp\apache\logs\error.log (Windows)
```

### MySQL Error Log:

```
/var/log/mysql/error.log
```

---

## 🆘 When to Contact Support

Contact ITM UiTM if:

- Server is down
- Database server issues
- DNS problems
- SSL certificate issues
- Hosting quota exceeded
- Security breaches
- Critical errors you can't fix

**Contact:**

- Email: itm@uitm.edu.my
- Phone: [Insert number]
- Ticket System: [Insert URL]

---

## 📋 Incident Report Template

When reporting issues:

```
Subject: [URGENT] Website Down - [Your Site Name]

Details:
- Site URL:
- Issue:
- When started:
- Steps taken:
- Error messages:
- Impact:
- Screenshots: (attach)
- Contact:
```

---

## 🛠️ Essential Tools

### Browser Tools:

- Chrome DevTools (F12)
- Firefox Developer Tools
- Browser Console

### Online Tools:

- **Down Detector:** Check if site is down
- **SSL Checker:** Verify SSL certificate
- **DNS Lookup:** Check DNS records
- **Pingdom:** Test from multiple locations

### Desktop Tools:

- **FileZilla:** FTP client
- **phpMyAdmin:** Database management
- **Notepad++:** Code editor
- **WinSCP:** Secure file transfer

---

## 💡 Preventive Measures

1. **Regular Backups**

   - Daily automated backups
   - Test restore procedures

2. **Keep Updated**

   - CMS core
   - Extensions/plugins
   - PHP version

3. **Monitor Performance**

   - Use uptime monitoring
   - Set up alerts
   - Check logs regularly

4. **Security Scanning**
   - Regular security scans
   - Malware detection
   - Vulnerability assessment

---

## 📖 Sumber Tambahan

- [Joomla Forum](https://forum.joomla.org)
- [Stack Overflow](https://stackoverflow.com)
- [UiTM ITM Knowledge Base](#)

---

## 📞 Emergency Contacts

**ITM UiTM Support**  
Email: itm@uitm.edu.my  
Phone: [Insert number]

**After Hours:**  
On-call: [Insert number]

---

_Dokumen ini dikemaskini secara berkala. Sila rujuk versi terkini._
