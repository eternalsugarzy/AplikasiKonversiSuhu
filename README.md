
# Aplikasi Konversi Suhu

Tugas 2 Modul Aplikasi Konversi Suhu

# Deskripsi
Aplikasi Konversi Suhu ini adalah program GUI sederhana yang dibuat menggunakan Java Swing dan NetBeans untuk membantu melakukan konversi suhu antara beberapa skala: Celcius, Fahrenheit, Reamur, dan Kelvin.


# Features

Fitur tambahan dari aplikasi ini meliputi:

1. Input Suhu: Pengguna dapat memasukkan suhu yang ingin dikonversi.
2. Pilih Skala Awal: Pengguna dapat memilih skala awal suhu yang ingin dikonversi (Celcius, Fahrenheit, Kelvin, atau Reamur).
3. Pilih Skala Tujuan: Pengguna dapat memilih skala tujuan untuk konversi suhu (Celcius, Fahrenheit, Kelvin, atau Reamur).
4. Konversi Otomatis: Aplikasi secara otomatis mengonversi suhu setelah input atau pilihan skala berubah.
5. Tombol Konversi Manual: Pengguna juga dapat memilih untuk melakukan konversi dengan menekan tombol "Konversi".
6. Hasil Konversi: Hasil konversi ditampilkan dalam bentuk teks di area output.


# Dokumentasi Code

```java
import java.awt.event.ActionListener;
import java.awt.event.ActionEvent;
import javax.swing.event.DocumentEvent;
import javax.swing.event.DocumentListener;


public class AplikasiKonversiSuhuForm extends javax.swing.JFrame {

    private String arahKonversi = "CtoF"; // Default arah konversi
    private double suhuInput; // Untuk menyimpan nilai input suhu
    private double hasilKonversi; // Untuk menyimpan hasil konversi

    public AplikasiKonversiSuhuForm() {
        initComponents();
        setupListeners(); // Mengatur listener
    }
    
    private void setupListeners() {
    // Listener untuk tombol konversi
    tombolKonversi.addActionListener(e -> lakukanKonversi());
    
    // Listener untuk JTextField agar mendeteksi perubahan input suhu
    textFieldSuhu.getDocument().addDocumentListener(new DocumentListener() {
        @Override
        public void insertUpdate(DocumentEvent e) {
            lakukanKonversi(); // Panggil metode konversi saat ada perubahan
        }

        @Override
        public void removeUpdate(DocumentEvent e) {
            lakukanKonversi(); // Panggil metode konversi saat ada perubahan
        }

        @Override
        public void changedUpdate(DocumentEvent e) {
            lakukanKonversi(); // Panggil metode konversi saat ada perubahan
        }
    });

    // Listener untuk RadioButton Fahrenheit
    radioButtonFahrenheit.addActionListener(e -> {
        arahKonversi = "toF"; // Konversi ke Fahrenheit
        lakukanKonversi(); // Panggil metode konversi saat pilihan diubah
    });

    // Listener untuk RadioButton Reamur
    radioButtonReamur.addActionListener(e -> {
        arahKonversi = "toR"; // Konversi ke Reamur
        lakukanKonversi(); // Panggil metode konversi saat pilihan diubah
    });

    // Listener untuk RadioButton Kelvin
    radioButtonKelvin.addActionListener(e -> {
        arahKonversi = "toK"; // Konversi ke Kelvin
        lakukanKonversi(); // Panggil metode konversi saat pilihan diubah
    });
    
    // Listener untuk RadioButton Kelvin
    radioButtonCelcius.addActionListener(e -> {
        arahKonversi = "toC"; // Konversi ke Celcius
        lakukanKonversi(); // Panggil metode konversi saat pilihan diubah
    });

    // Listener untuk ComboBox Konversi Dari
    comboBoxKonversiDari.addActionListener(e -> {
        lakukanKonversi(); // Panggil metode konversi saat pilihan diubah
    });
}

    
     private void lakukanKonversi() {
    try {
        // Mengambil nilai dari JTextField
        suhuInput = Double.parseDouble(textFieldSuhu.getText());

        // Mendapatkan pilihan dari ComboBox
        String konversiDari = comboBoxKonversiDari.getSelectedItem().toString();

        // Melakukan konversi berdasarkan arah konversi
        switch (konversiDari) {
            case "Celcius":
                if (arahKonversi.equals("toF")) {
                    hasilKonversi = suhuInput * 9/5 + 32; // Celcius ke Fahrenheit
                } else if (arahKonversi.equals("toR")) {
                    hasilKonversi = suhuInput * 4/5; // Celcius ke Reamur
                } else if (arahKonversi.equals("toK")) {
                    hasilKonversi = suhuInput + 273.15; // Celcius ke Kelvin
                }
                break;
            case "Fahrenheit":
                if (arahKonversi.equals("toC")) {
                    hasilKonversi = (suhuInput - 32) * 5/9; // Fahrenheit ke Celcius
                } else if (arahKonversi.equals("toR")) {
                    hasilKonversi = (suhuInput - 32) * 4/9; // Fahrenheit ke Reamur
                } else if (arahKonversi.equals("toK")) {
                    hasilKonversi = (suhuInput - 32) * 5/9 + 273.15; // Fahrenheit ke Kelvin
                }
                break;
            case "Reamur":
                if (arahKonversi.equals("toC")) {
                    hasilKonversi = suhuInput * 5/4; // Reamur ke Celcius
                } else if (arahKonversi.equals("toF")) {
                    hasilKonversi = suhuInput * 9/4 + 32; // Reamur ke Fahrenheit
                } else if (arahKonversi.equals("toK")) {
                    hasilKonversi = suhuInput * 5/4 + 273.15; // Reamur ke Kelvin
                }
                break;
            case "Kelvin":
                if (arahKonversi.equals("toC")) {
                    hasilKonversi = suhuInput - 273.15; // Kelvin ke Celcius
                } else if (arahKonversi.equals("toF")) {
                    hasilKonversi = (suhuInput - 273.15) * 9/5 + 32; // Kelvin ke Fahrenheit
                } else if (arahKonversi.equals("toR")) {
                    hasilKonversi = (suhuInput - 273.15) * 4/5; // Kelvin ke Reamur
                }
                break;
            default:
                hasilKonversi = suhuInput; // Jika tidak ada konversi
                break;
        }

        // Menampilkan hasil konversi di label output
        labelHasil.setText(String.format("Hasil: %.2f", hasilKonversi));
    } catch (NumberFormatException ex) {
        // Tampilkan pesan kesalahan jika input tidak valid
        labelHasil.setText("Masukkan angka yang valid.");
    }
}

    /**
     * This method is called from within the constructor to initialize the form.
     * WARNING: Do NOT modify this code. The content of this method is always
     * regenerated by the Form Editor.
     */
    @SuppressWarnings("unchecked")
    // <editor-fold defaultstate="collapsed" desc="Generated Code">                          
    private void initComponents() {

        buttonGroup1 = new javax.swing.ButtonGroup();
        jPanel1 = new javax.swing.JPanel();
        jLabel1 = new javax.swing.JLabel();
        jLabel2 = new javax.swing.JLabel();
        labelHasil = new javax.swing.JLabel();
        textFieldSuhu = new javax.swing.JTextField();
        comboBoxKonversiDari = new javax.swing.JComboBox<>();
        jLabel4 = new javax.swing.JLabel();
        jLabel5 = new javax.swing.JLabel();
        radioButtonFahrenheit = new javax.swing.JRadioButton();
        radioButtonReamur = new javax.swing.JRadioButton();
        radioButtonKelvin = new javax.swing.JRadioButton();
        tombolKonversi = new javax.swing.JButton();
        radioButtonCelcius = new javax.swing.JRadioButton();

        setDefaultCloseOperation(javax.swing.WindowConstants.EXIT_ON_CLOSE);

        jLabel1.setFont(new java.awt.Font("Verdana", 1, 18)); // NOI18N
        jLabel1.setText("Aplikasi Konversi Suhu");

        jLabel2.setText("Masukan Suhu:");

        labelHasil.setText("Hasil Konversi");

        textFieldSuhu.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                textFieldSuhuActionPerformed(evt);
            }
        });

        comboBoxKonversiDari.setModel(new javax.swing.DefaultComboBoxModel<>(new String[] { "Celcius", "Fahrenheit", "Kelvin", "Reamur" }));

        jLabel4.setText("Konversi Dari:");

        jLabel5.setText("Konversi ke:");

        buttonGroup1.add(radioButtonFahrenheit);
        radioButtonFahrenheit.setText("Fahrenheit");

        buttonGroup1.add(radioButtonReamur);
        radioButtonReamur.setText("Reamur");

        buttonGroup1.add(radioButtonKelvin);
        radioButtonKelvin.setText("Kelvin");
        radioButtonKelvin.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                radioButtonKelvinActionPerformed(evt);
            }
        });

        tombolKonversi.setText("Konversi");
        tombolKonversi.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                tombolKonversiActionPerformed(evt);
            }
        });

        buttonGroup1.add(radioButtonCelcius);
        radioButtonCelcius.setText("Celcius");

        javax.swing.GroupLayout jPanel1Layout = new javax.swing.GroupLayout(jPanel1);
        jPanel1.setLayout(jPanel1Layout);
        jPanel1Layout.setHorizontalGroup(
            jPanel1Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGroup(jPanel1Layout.createSequentialGroup()
                .addGroup(jPanel1Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                    .addGroup(jPanel1Layout.createSequentialGroup()
                        .addContainerGap()
                        .addGroup(jPanel1Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                            .addComponent(jLabel1)
                            .addGroup(jPanel1Layout.createSequentialGroup()
                                .addComponent(jLabel4)
                                .addGap(100, 100, 100)
                                .addComponent(comboBoxKonversiDari, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE))
                            .addComponent(jLabel5)
                            .addGroup(jPanel1Layout.createSequentialGroup()
                                .addComponent(jLabel2)
                                .addGap(92, 92, 92)
                                .addComponent(textFieldSuhu, javax.swing.GroupLayout.PREFERRED_SIZE, 128, javax.swing.GroupLayout.PREFERRED_SIZE))))
                    .addGroup(jPanel1Layout.createSequentialGroup()
                        .addGap(190, 190, 190)
                        .addGroup(jPanel1Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                            .addGroup(jPanel1Layout.createSequentialGroup()
                                .addComponent(radioButtonFahrenheit)
                                .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.UNRELATED)
                                .addComponent(radioButtonReamur)
                                .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.RELATED)
                                .addComponent(radioButtonKelvin)
                                .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.UNRELATED)
                                .addComponent(radioButtonCelcius))
                            .addGroup(jPanel1Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.TRAILING)
                                .addComponent(labelHasil)
                                .addComponent(tombolKonversi)))))
                .addContainerGap(150, Short.MAX_VALUE))
        );
        jPanel1Layout.setVerticalGroup(
            jPanel1Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGroup(jPanel1Layout.createSequentialGroup()
                .addGap(24, 24, 24)
                .addComponent(jLabel1)
                .addGap(31, 31, 31)
                .addGroup(jPanel1Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.BASELINE)
                    .addComponent(textFieldSuhu, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE)
                    .addComponent(jLabel2))
                .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.RELATED)
                .addGroup(jPanel1Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.BASELINE)
                    .addComponent(comboBoxKonversiDari, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE)
                    .addComponent(jLabel4))
                .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.UNRELATED)
                .addGroup(jPanel1Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.BASELINE)
                    .addComponent(jLabel5)
                    .addComponent(radioButtonFahrenheit)
                    .addComponent(radioButtonReamur)
                    .addComponent(radioButtonKelvin)
                    .addComponent(radioButtonCelcius))
                .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.UNRELATED)
                .addComponent(tombolKonversi)
                .addGap(32, 32, 32)
                .addComponent(labelHasil)
                .addContainerGap(205, Short.MAX_VALUE))
        );

        javax.swing.GroupLayout layout = new javax.swing.GroupLayout(getContentPane());
        getContentPane().setLayout(layout);
        layout.setHorizontalGroup(
            layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGroup(layout.createSequentialGroup()
                .addContainerGap()
                .addComponent(jPanel1, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, Short.MAX_VALUE)
                .addContainerGap())
        );
        layout.setVerticalGroup(
            layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGroup(layout.createSequentialGroup()
                .addContainerGap()
                .addComponent(jPanel1, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, Short.MAX_VALUE)
                .addContainerGap())
        );

        pack();
    }// </editor-fold>                        

    private void tombolKonversiActionPerformed(java.awt.event.ActionEvent evt) {                                               
        // TODO add your handling code here:
    }                                              

    private void radioButtonKelvinActionPerformed(java.awt.event.ActionEvent evt) {                                                  
        // TODO add your handling code here:
    }                                                 

    private void textFieldSuhuActionPerformed(java.awt.event.ActionEvent evt) {                                              
        // TODO add your handling code here:
    }                                             

    /**
     * @param args the command line arguments
     */
    public static void main(String args[]) {
        /* Set the Nimbus look and feel */
        //<editor-fold defaultstate="collapsed" desc=" Look and feel setting code (optional) ">
        /* If Nimbus (introduced in Java SE 6) is not available, stay with the default look and feel.
         * For details see http://download.oracle.com/javase/tutorial/uiswing/lookandfeel/plaf.html 
         */
        try {
            for (javax.swing.UIManager.LookAndFeelInfo info : javax.swing.UIManager.getInstalledLookAndFeels()) {
                if ("Nimbus".equals(info.getName())) {
                    javax.swing.UIManager.setLookAndFeel(info.getClassName());
                    break;
                }
            }
        } catch (ClassNotFoundException ex) {
            java.util.logging.Logger.getLogger(AplikasiKonversiSuhuForm.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        } catch (InstantiationException ex) {
            java.util.logging.Logger.getLogger(AplikasiKonversiSuhuForm.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        } catch (IllegalAccessException ex) {
            java.util.logging.Logger.getLogger(AplikasiKonversiSuhuForm.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        } catch (javax.swing.UnsupportedLookAndFeelException ex) {
            java.util.logging.Logger.getLogger(AplikasiKonversiSuhuForm.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        }
        //</editor-fold>

        /* Create and display the form */
        java.awt.EventQueue.invokeLater(new Runnable() {
            public void run() {
                new AplikasiKonversiSuhuForm().setVisible(true);
            }
        });
    }

    // Variables declaration - do not modify                     
    private javax.swing.ButtonGroup buttonGroup1;
    private javax.swing.JComboBox<String> comboBoxKonversiDari;
    private javax.swing.JLabel jLabel1;
    private javax.swing.JLabel jLabel2;
    private javax.swing.JLabel jLabel4;
    private javax.swing.JLabel jLabel5;
    private javax.swing.JPanel jPanel1;
    private javax.swing.JLabel labelHasil;
    private javax.swing.JRadioButton radioButtonCelcius;
    private javax.swing.JRadioButton radioButtonFahrenheit;
    private javax.swing.JRadioButton radioButtonKelvin;
    private javax.swing.JRadioButton radioButtonReamur;
    private javax.swing.JTextField textFieldSuhu;
    private javax.swing.JButton tombolKonversi;
    // End of variables declaration                   

    
}





```


## Authors

Muhammad Irwan Firmanto
2210010582 5B Reg Pagi Banjarmasin

- [@eternalsugarzy](https://www.github.com/eternalsugarzy)


## Screenshots


![Screenshot 2024-11-02 234519](https://github.com/user-attachments/assets/a0465907-b7e9-44f4-89a6-53ec828a63a5)

