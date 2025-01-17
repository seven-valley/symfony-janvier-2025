# Créer un PDF
la documentation
http://www.fpdf.org/

# Etape 1 Installer recipe
```
composer require setasign/fpdf
```

# Etape 2 créer une route
```php
 #[Route('/pdf', name: 'app_pdf')]
    public function pdf(): Response
    {
        $pdf = new \FPDF();
        $pdf->AddPage();
        $pdf->SetFont('Arial');
        // Cell(float w [, float h [, string txt [, mixed border [, int ln [, string align [, boolean fill [, mixed link]]]]]]])
        $pdf->Cell(40, 10, 'Hello World', 1, 2);
        return new Response($pdf->Output("Facture 001.pdf", "I"), 200, array(
            'Content-Type' => 'application/pdf'
        ));
    }
```


```php
#[Route('/pdf', name: 'app_pdf')]
    public function pdf(): Response
    {
        $pdf = new \FPDF();
        $pdf->AddPage();
        $pdf->SetFont('Arial');
        // Cell(float w [, float h [, string txt [, mixed border [, int ln [, string align [, boolean fill [, mixed link]]]]]]])
        $pdf->SetFillColor(200,200,200);
        $pdf->Cell(40, 10, 'Hello World', 1, 2,'C',1);
        return new Response($pdf->Output("Facture 001.pdf", "I"), 200, array(
            'Content-Type' => 'application/pdf'
        ));
    }
```