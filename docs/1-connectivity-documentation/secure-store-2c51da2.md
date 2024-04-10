<!-- loio2c51da23ded24eb4a50d9b630ccd8b91 -->

# Secure Store

Reduce the size of the Cloud Connector Secure Store.

The Secure Store is a container for confidential information that is a part of the Cloud Connector configuration. The Secure Store resides in file `SSFS_SCC.DAT`, located in directory *scc\_config*.

Every change affecting the Secure Store \(such as changing the proxy password\) is incremental, that is, it is appended to the Secure Store. As a consequence, the Secure Store will grow over time.

At some point it is sensible to remove obsolete entries to reduce the size of the Secure Store, and hence the size of the file `SSFS_SCC.DAT`.

To do this, choose *Configuration* \> *Shrink Secure Store* \(top right corner of the screen\) from the Cloud Connector main menu.

