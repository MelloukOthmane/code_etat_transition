# code_etat_transition
enum EtatLivre
{
    Commande,
    Reçu,
    Enregistre,
    Disponible,
    Emprunte,
    EnRetard,
    Prolongation,
    Reserve,
    Indisponible,
    Endommage,
    Restaurer,
    Archive
}

class Livre
{
    public EtatLivre Etat {get; private set;}
    public int NombreEmprunt {get; private set;}
    public DateTime DateEmprunt {get; private set;}
    public DateTime DateRetour {get; private set;}

    public Livre()
    {
        Etat = EtatLivre.Commande;
    }

    public void Commander()
    {
        if (Etat != EtatLivre.Commande)
        {
            Etat = EtatLivre.Commande;
        }
    }

    public void Recevoir()
    {
        if (Etat == EtatLivre.Commande)
        {
            Etat = EtatLivre.Reçu;
        }
    }

    public void Enregistrer()
    {
        if (Etat == EtatLivre.Reçu)
        {
            Etat = EtatLivre.Enregistre;
        }
    }

    public void MettreDisponible()
    {
        if (Etat == EtatLivre.Enregistre)
        {
            Etat = EtatLivre.Disponible;
        }
    }

    public void Emprunter(DateTime dateEmprunt)
    {
        if (Etat == EtatLivre.Disponible)
        {
            Etat = EtatLivre.Emprunte;
            DateEmprunt = dateEmprunt;
            DateRetour = dateEmprunt.AddDays(14);
            NombreEmprunt++;
        }
    public void Retourner()
{
    if (Etat == EtatLivre.Emprunte)
    {
        Etat = EtatLivre.Disponible;
        DateEmprunt = DateTime.MinValue;
        DateRetour = DateTime.MinValue;
    }
}

public void Prolonger(DateTime dateProlongation)
{
    if (Etat == EtatLivre.Emprunte)
    {
        Etat = EtatLivre.Prolongation;
        DateRetour = dateProlongation;
    }
}

public void Reserver()
{
    if (Etat == EtatLivre.Disponible)
    {
        Etat = EtatLivre.Reserve;
    }
}

public void Indisponible()
{
    if (Etat != EtatLivre.Indisponible)
    {
        Etat = EtatLivre.Indisponible;
    }
}

public void Endommager()
{
    if (Etat != EtatLivre.Endommage)
    {
        Etat = EtatLivre.Endommage;
    }
}

public void Restaurer()
{
    if (Etat == EtatLivre.Endommage)
    {
        Etat = EtatLivre.Restaurer;
    }
}

public void Archiver()
{
    if (Etat != EtatLivre.Archive)
    {
        Etat = EtatLivre.Archive;
    }
}
    
}
