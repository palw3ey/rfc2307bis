# rfc2307bis

nis rfc2307 is obsolete, this README will help you to replace it by the new rfc2307bis.ldif

# 1) Install openldap and utils

sudo apt install slapd ldap-utils

# 2) Download rfc2307bis.ldif

sudo wget https://github.com/palw3ey/rfc2307bis/releases/download/latest/rfc2307bis.ldif -O /etc/ldap/schema/rfc2307bis.ldif

# 3) Edit slapd.init.ldif to replace rfc2307

sudo vim /usr/share/slapd/slapd.init.ldif

find this line : include: file:///etc/ldap/schema/nis.ldif

append a # at the beginning of the line, to make it as a comment


and just below this commented line, add :

include: file:///etc/ldap/schema/rfc2307bis.ldif

# 4) Start the configuration of openldap

sudo dpkg-reconfigure slapd

# 5) Verify that rfc2307bis is enabled

sudo ldapsearch -LLL -Y external -H ldapi:/// -b cn=schema,cn=config -s one dn

If everything is OK, then you should see this line in the output : dn: cn={2}rfc2307bis,cn=schema,cn=config

