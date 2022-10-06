

# TP 5 - Systèmes de fichiers, partitions et disques

  

## Exercice 1. Disques et partitions

2. Vérifiez que ce nouveau disque dur est bien détecté par le système
Lister les disques et les partitions
lsblk : liste les périphériques en mode bloc, et donc les disques et partitions :
  
```  
ll /dev/sd*
```  
  

3. Partitionnez ce disque en utilisant fdisk : créez une première partition de 2 Go de type Linux (n°83), et une seconde partition de 3 Go en NTFS (n°7)
Lister les partitions :
```  
sudo fdisk -l
```  
  
pour crée une partition :
```  
sudo fdisk /dev/sdb
N
P 
+2G pour indiqué 2GO

```  

Pour modifié un disque :
t -> sélectionné le disque -> mettre le numéro d'alias (Linux (n°83), NTFS (n°7))
W pour sauvegardé

  

4. A ce stade, les partitions ont été créées, mais elles n’ont pas été formatées avec leur système de fichiers. A l’aide de la commande mkfs, formatez vos deux partitions

Pour formaté
```
sudo mkfs.ext4 /dev/sdb1
sudo mkfs.ntfs /dev/sdb2
```
  
  

5. Pourquoi la commande df -T, qui affiche le type de système de fichier des partitions, ne fonctionne-telle pas sur notre disque ?

df -T, qui affiche le type de système de fichier des partitions

ne fonctionne pas si les partition ne sont pas monté *

  

6. Faites en sorte que les deux partitions créées soient montées automatiquement au démarrage de la machine, respectivement dans les points de montage /data et /win (vous pourrez vous passer des UUID en raison de l’impossibilité d’effectuer des copier-coller)
```
sudo mount /dev/sdb1 /data
sudo mount /dev/sdb2 /win
```
```
sudo nano /etc/fstab
```
/dev/sdb1 /data linux defaults 0
/dev/sdb2 /win ntfs  defaults 0

7. Utilisez la commande mount puis redémarrez votre VM pour valider la configuration

mount validé la config avant de redemaré

  
  

## Exercice 2. Partitionnement LVM

  

1. On va réutiliser le disque de 5 Gio de l’exercice précédent. Commencez par démonter les systèmes de fichiers montés dans /data et /win s’ils sont encore montés, et supprimez les lignes correspondantes du fichier /etc/fstab
```
sudo umount /data
```
  

2. Supprimez les deux partitions du disque, et créez une partition unique de type LVM
```
sudo fdisk /dev/sdb
```
d pour supprimé
w pour sauvegardé

  

3. A l’aide de la commande pvcreate, créez un volume physique LVM. Validez qu’il est bien créé, en utilisant la commande pvdisplay.
```
sudo pvcreate /dev/sdb
sudo pvdisplay
```
4. A l’aide de la commande vgcreate, créez un groupe de volumes, qui pour l’instant ne contiendra que le volume physique créé à l’étape précédente. Vérifiez à l’aide de la commande vgdisplay.
```
sudo vgcreate GRP /dev/sdb
vgdisplay
```
5. Créez un volume logique appelé lvData occupant l’intégralité de l’espace disque disponible
```
sudo lvcreate -l 100%FREE -n lvData GRP
```
6. Dans ce volume logique, créez une partition que vous formaterez en ext4, puis procédez comme dans l’exercice 1 pour qu’elle soit montée automatiquement, au démarrage de la machine, dans /data


8. Utilisez la commande vgextend pour ajouter le nouveau disque au groupe de

vgextend pour ajouter le nouveau disque au groupe de volumes

